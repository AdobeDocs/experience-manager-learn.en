---
title: Best practices for Traffic Filter rules including WAF rules
description: Learn recommended best practices for Traffic Filter rules including WAF rules.
version: Cloud Service
feature: Security
topic: Security, Administration, Architecture
role: Admin, Architect
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2023-10-26
jira: KT-13148
thumbnail: KT-13148.jpeg
exl-id: 4a7acdd2-f442-44ee-8560-f9cb64436acf
duration: 194
---
# Best practices for traffic filter rules including WAF rules

Learn recommended best practices for traffic filter rules, including WAF rules. It is important to note that the best practices described in this article are not exhaustive and are not intended to be a substitute for your own security policies and procedures.

>[!VIDEO](https://video.tv.adobe.com/v/3425408?quality=12&learn=on)

## General best practices

- To determine which rules are appropriate for your organization, collaborate with your security team.
- Always test rules in Dev environments before deploying them to Stage and Production environments.
- When declaring and validating rules, always start with `action` type `log` to ensure that the rule is not blocking legitimate traffic.
- For certain rules, the transition from `log` to `block` should be purely based on analysis of sufficient site traffic.
- Introduce rules incrementally, and consider involving your testing teams (QA, performance, penetration testing) in the process.
- Analyze the impact of rules regularly using the [dashboard tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-ELK-Tool). Depending on your site's traffic volume, the analysis can be done daily, weekly, or monthly.
- To block malicious traffic that you may be aware of after the analysis, add any additional rules. For example, certain IPs that have been attacking your site.
- Rule creation, deployment, and analysis should be an ongoing, iterative process. It is not a one-time activity.

## Best practices for traffic filter rules

Enable the traffic filter rules below for your AEM project. However the desired values for `rateLimit` and `clientCountry` properties must be determined in collaboration with your security team.

```yaml
kind: CDN
version: '1'
metadata:
  envTypes:
    - dev
    - stage
    - prod
data:
  trafficFilters:
    rules:
    #  Prevent DoS attacks by blocking client for 5 minutes if they make more than 100 requests in 1 second.
      - name: prevent-dos-attacks
        when:
          reqProperty: path
          like: '*'
        rateLimit:
          limit: 100
          window: 1
          penalty: 300
          groupBy:
            - reqProperty: clientIp
        action: block
    # Block requests coming from OFAC countries
      - name: block-ofac-countries
        when:
          allOf:
              - reqProperty: tier
              - matches: publish
              - reqProperty: clientCountry
                in:
                  - SY
                  - BY
                  - MM
                  - KP
                  - IQ
                  - CD
                  - SD
                  - IR
                  - LR
                  - ZW
                  - CU
                  - CI
```

>[!WARNING]
>
>For your production environment, collaborate with your Web Security team to determine the appropriate values for `rateLimit`

## Best practices for WAF rules

Once the WAF is licensed and enabled for your program, traffic matching WAF flags appear in charts and request logs, even if you didn't declare them in a rule. This is so you are always aware of potentially new malicious traffic and can create rules as needed. Look at WAF flags that are not reflected in the declared rules and consider declaring them.

Consider the WAF rules below for your AEM project. However the desired values for `action` and `wafFlags` property must be determined in collaboration with your security team.

```yaml
kind: CDN
version: '1'
metadata:
  envTypes:
    - dev
    - stage
    - prod
data:
  trafficFilters:
    rules:

    # Traffic Filter rules shown in above section
    ...

    # Enable WAF protections (only works if WAF is enabled for your environment)
      - name: block-waf-flags
        when:
          reqProperty: tier
          matches: "author|publish"
        action:
          type: block
          wafFlags:
            - SANS
            - TORNODE
            - NOUA
            - SCANNER
            - USERAGENT
            - PRIVATEFILE
            - ABNORMALPATH
            - TRAVERSAL
            - NULLBYTE
            - BACKDOOR
            - LOG4J-JNDI
            - SQLI
            - XSS
            - CODEINJECTION
            - CMDEXE
            - NO-CONTENT-TYPE
            - UTF8
    # Disable protection against CMDEXE on /bin
      - name: allow-cdmexe-on-root-bin
        when:
          allOf:
            - reqProperty: tier
              matches: "author|publish"
            - reqProperty: path
              matches: "^/bin/.*"
        action:
          type: allow
          wafFlags:
            - CMDEXE
```

## Summary

In conclusion, this tutorial has equipped you with the knowledge and tools needed to bolster the security of your web applications in Adobe Experience Manager as a Cloud Service (AEMCS). With practical rule examples and insights into result analysis, you can effectively protect your website and applications.



