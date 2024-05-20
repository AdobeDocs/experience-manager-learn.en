---
title: CDN cache hit ratio analysis
description: Learn how to analyze the AEM as a Cloud Service provided CDN logs. Gain insights such as cache hit ratio, and top URLs of MISS and PASS cache types for optimization purposes.
version: Cloud Service
feature: Operations, CDN Cache
topic: Administration, Performance
role: Admin, Architect, Developer
level: Intermediate
doc-type: Tutorial
last-substantial-update: 2023-11-10
jira: KT-13312
thumbnail: KT-13312.jpeg
exl-id: 43aa7133-7f4a-445a-9220-1d78bb913942
duration: 276
---
# CDN cache hit ratio analysis

Content cached at the CDN reduces the latency experienced by website users, who do not need to wait for the request to make its way back to the Apache/dispatcher or AEM publish. With that in mind, it is worthwhile to optimize the CDN cache hit ratio to maximize the amount of content cacheable at the CDN.

Learn how to analyze the AEM as a Cloud Service provided **CDN logs** and gain insights such as **cache hit ratio**, and **top URLs of _MISS_ and _PASS_ cache types**, for optimization purposes.


The CDN logs are available in JSON format, which contains various fields including `url`, `cache`. For more information, see the [CDN Log Format](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/logging.html?lang=en#cdn-log:~:text=Toggle%20Text%20Wrapping-,Log%20Format,-The%20CDN%20logs). The `cache` field provides information about _state of the cache_ and its possible values are HIT, MISS, or PASS. Let's review the details of possible values.

| State of Cache </br> Possible Value                                                   | Description |
|------------------------------------|:-----------------------------------------------------:|
| HIT | The requested data is _found in the CDN cache and does not require making a fetch_ request to the AEM server. |
| MISS | The requested data is _not found in the CDN cache and has to be requested_ from the AEM server. |
| PASS | The requested data is _explicitly set not to be cached_ and always be retrieved from the AEM server. |

For the purpose of this tutorial, the [AEM WKND project](https://github.com/adobe/aem-guides-wknd) is deployed to the AEM as a Cloud Service environment and a small performance test is triggered using [Apache JMeter](https://jmeter.apache.org/).

This tutorial is structured to take you through the following process:

1. Downloading CDN logs via Cloud Manager
1. Analyzing those CDN logs, it can be performed with two approaches: a locally installed dashboard or a remotely accessed Splunk or Jupityer Notebook (for those who license Adobe Experience Platform)
1. Optimizing CDN cache configuration

## Download CDN logs

To download the CDN logs, follow these steps:

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select your organization and program.

1. For a desired AEMCS environment, select **Download Logs** from the ellipsis menu.

    ![Download Logs - Cloud Manager](assets/cdn-logs-analysis/download-logs.png){width="500" zoomable="yes"}

1. In the **Download Logs** dialog, select the **Publish** Service from the drop-down menu, then click the download icon next to the **CDN** row.

    ![CDN Logs - Cloud Manager](assets/cdn-logs-analysis/download-cdn-logs.png){width="500" zoomable="yes"}


If the downloaded log file is from _today_ the file extension is `.log` otherwise for past log files the extension is `.log.gz`.

## Analyze downloaded CDN logs

To gain insights such as cache hit ratio, and top URLs of MISS and PASS cache types, analyze the downloaded CDN log file. These insights help to optimize the [CDN cache configuration](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching) and enhance the site performance.

To analyze the CDN logs, this tutorial presents three options:  

1. **Elasticsearch, Logstash, and Kibana (ELK)**: The [ELK dashboard tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling/blob/main/ELK/README.md) can be installed locally. 
1. **Splunk**: The [Splunk dashboard tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling/blob/main/Splunk/README.md) requires access to Splunk and [AEMCS log forwarding enabled](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/developing/logging#splunk-logs) to ingest the CDN logs.
1. **Jupyter Notebook**: It can be accessed remotely as part of [Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/data-science-workspace/jupyterlab/analyze-your-data) without installing additional software, for customers who have licensed Adobe Experience Platform.

### Option 1: Using ELK dashboard tooling

The [ELK stack](https://www.elastic.co/elastic-stack) is a set of tools that provide a scalable solution to search, analyze, and visualize the data. It consists of Elasticsearch, Logstash, and Kibana.

To identify the key details, let's use the [AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling) project. This project provides a Docker container of the ELK stack and a pre-configured Kibana dashboard to analyze the CDN logs.

1. Follow the steps from [How to set up the ELK Docker container](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling/blob/main/ELK/README.md#how-to-set-up-the-elk-docker-containerhow-to-setup-the-elk-docker-container) and make sure to import the **CDN Cache Hit Ratio** Kibana dashboard.

1. To identify the CDN cache hit ratio and top URLs, follow these steps:

    1. Copy the downloaded CDN log file/s inside the environment-specific logs folder, for example, `ELK/logs/stage`.

    1. Open the **CDN Cache Hit Ratio** dashboard by clicking the top-left corner _Navigation Menu > Analytics > Dashboard > CDN Cache Hit Ratio_.

        ![CDN Cache Hit Ratio - Kibana Dashboard](assets/cdn-logs-analysis/cdn-cache-hit-ratio-dashboard.png){width="500" zoomable="yes"}

    1. Select the desired time range from the top-right corner.

        ![Time Range - Kibana Dashboard](assets/cdn-logs-analysis/time-range.png){width="500" zoomable="yes"}
    
    1. The **CDN Cache Hit Ratio** dashboard is self-explanatory. 
    
    1. The _Total Request Analysis_ section displays the following details:
        - Cache ratios by cache type
        - Cache counts by cache type

        ![Total Request Analysis - Kibana Dashboard](assets/cdn-logs-analysis/total-request-analysis.png){width="500" zoomable="yes"}

    1. The _Analysis by Request or Mime Types_ displays the following details: 
        - Cache ratios by cache type
        - Cache counts by cache type
        - Top MISS and PASS URLs

        ![Analysis by Request or Mime Types - Kibana Dashboard](assets/cdn-logs-analysis/analysis-by-request-or-mime-types.png){width="500" zoomable="yes"}

#### Filtering by environment name or program ID

To filter the ingested logs by environment name, follow the below steps:

1. In the CDN Cache Hit Ratio dashboard, click the **Add Filter** icon.

    ![Filter - Kibana Dashboard](assets/cdn-logs-analysis/filter.png){width="500" zoomable="yes"}

1. In the **Add filter** modal, select the `aem_env_name.keyword` field from the drop-down menu, and `is` operator and desired environment name for next field and finally click _Add filter_.

    ![Add Filter - Kibana Dashboard](assets/cdn-logs-analysis/add-filter.png){width="500" zoomable="yes"}

#### Filtering by hostname

To filter the ingested logs by hostname, follow the below steps:

1. In the CDN Cache Hit Ratio dashboard, click the **Add Filter** icon.

    ![Filter - Kibana Dashboard](assets/cdn-logs-analysis/filter.png){width="500" zoomable="yes"}

1. In the **Add filter** modal, select the `host.keyword` field from the drop-down menu, and `is` operator and desired hostname for next field and finally click _Add filter_.

    ![Host Filter - Kibana Dashboard](assets/cdn-logs-analysis/add-host-filter.png){width="500" zoomable="yes"}

Likewise, add more filters to the dashboard based on the analysis requirements.

### Option 2: Using Splunk dashboard tooling

The [Splunk](https://www.splunk.com/) is a popular log analysis tool that helps aggregate, analyze logs, and create visualizations for monitoring and troubleshooting purposes.

To identify the key details, let's use the [AEMCS-CDN-Log-Analysis-Tooling](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling) project. This project provides a Splunk dashboard to analyze the CDN logs.

1. Follow the steps from [Splunk dashboards for AEMCS CDN Log Analysis](https://github.com/adobe/AEMCS-CDN-Log-Analysis-Tooling/blob/main/Splunk/README.md) and make sure to import the **CDN Cache Hit Ratio** Splunk dashboard.
1. If needed, update the _Index, Source Type and other_ filter values in the Splunk dashboard.

    ![Splunk Dashboard](assets/cdn-logs-analysis/splunk-CHR-dashboard.png){width="500" zoomable="yes"}

>[!NOTE]
>
>The UI and graphs in the splunk dashboard differ from the ELK dashboard, however, the key details are similar.

### Option 3: Using Jupyter Notebook

For those who would rather not install software locally (that is, the ELK dashboard tooling from the previous section), there is another option, but it requires a license to Adobe Experience Platform.

The [Jupyter Notebook](https://jupyter.org/) is an open-source web application that lets you create documents that contain code, text, and visualization. It is used for data transformation, visualization, and statistical modeling. It can be accessed remotely [as part of Adobe Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/data-science-workspace/jupyterlab/analyze-your-data).

#### Downloading the Interactive Python Notebook file

First, download the [AEM-as-a-CloudService - CDN Logs Analysis - Jupyter Notebook](./assets/cdn-logs-analysis/aemcs_cdn_logs_analysis.ipynb) file, which will help with the CDN logs analysis. This "Interactive Python Notebook" file is self-explanatory, however, the key highlights of each section are:

- **Install additional libraries**: installs the `termcolor` and `tabulate` Python libraries.
- **Load CDN logs**: loads the CDN log file using `log_file` variable value; make sure to update its value. It also transforms this CDN log into the [Pandas DataFrame](https://pandas.pydata.org/docs/reference/frame.html).
- **Perform analysis**: the first code block is _Display Analysis Result for Total, HTML, JS/CSS and Image Requests_; it provides cache hit ratio percentage, bar, and pie charts.
The second code block is _Top 5 MISS and PASS Request URLs for HTML, JS/CSS, and Image_; it displays URLs and their counts in table format.

#### Running the Jupyter Notebook

Next, run the Jupyter Notebook in Adobe Experience Platform, by following these steps:

1. Login to the [Adobe Experience Cloud](https://experience.adobe.com/), in the Home page > **Quick access** section > click the **Experience Platform**

    ![Experience Platform](assets/cdn-logs-analysis/experience-platform.png){width="500" zoomable="yes"}

1. In the Adobe Experience Platform Home page > Data Science section >, click the **Notebooks** menu item. To start the Jupyter Notebooks environment, click the **JupyterLab** tab. 

    ![Notebook Log File Value Update](assets/cdn-logs-analysis/datascience-notebook.png){width="500" zoomable="yes"}

1. In the JupyterLab menu, using the **Upload Files** icon, upload the downloaded CDN log file and `aemcs_cdn_logs_analysis.ipynb` file.

    ![Upload Files - JupyteLab](assets/cdn-logs-analysis/jupyterlab-upload-file.png){width="500" zoomable="yes"}

1. Open the `aemcs_cdn_logs_analysis.ipynb` file by double-clicking.

1. In the **Load CDN Log File** section of the notebook, update the `log_file` value.

    ![Notebook Log File Value Update](assets/cdn-logs-analysis/notebook-update-variable.png){width="500" zoomable="yes"}

1. To run the selected cell and advance, click the **Play** icon. 
    
    ![Notebook Log File Value Update](assets/cdn-logs-analysis/notebook-run-cell.png){width="500" zoomable="yes"}

1. After running the **Display Analysis Result for Total, HTML, JS/CSS, and Image Requests** code cell, the output displays the cache hit ratio percentage, bar, and pie charts.
    
    ![Notebook Log File Value Update](assets/cdn-logs-analysis/output-cache-hit-ratio.png){width="500" zoomable="yes"}

1. After running the **Top 5 MISS and PASS Request URLs for HTML, JS/CSS, and Image** code cell, the output displays the Top 5 MISS and PASS Request URLs.

    ![Notebook Log File Value Update](assets/cdn-logs-analysis/output-top-urls.png){width="500" zoomable="yes"}

You can enhance the Jupyter Notebook to analyze the CDN logs based on your requirements.

## Optimizing CDN cache configuration

After analyzing the CDN logs, you can optimize the CDN cache configuration to improve the site performance. The AEM best practice is to have a cache hit ratio of 90% or higher.

For more information, see [Optimize CDN Cache Configuration](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/caching).

The AEM WKND project has a reference CDN configuration, for more information, see [CDN Configuration](https://github.com/adobe/aem-guides-wknd/blob/main/dispatcher/src/conf.d/available_vhosts/wknd.vhost#L137-L190) from the `wknd.vhost` file.
