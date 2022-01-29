---
title: Explore the AEM GraphQL API - Advanced Concepts of AEM Headless - GraphQL
description: Send GraphQL queries using the GraphiQL IDE. Learn about advanced queries using filters, variables, and directives. Query for fragment and content references including references from multi-line text fields.
version: Cloud Service
feature: Content Fragments, GraphQL API
topic: Headless, Content Management
role: Developer
level: Intermediate
exl-id: bd7916be-8caa-4321-add0-4c9031306d60
---
# Explore the AEM GraphQL API

The GraphQL API in AEM allows you to expose Content Fragment data to downstream applications. In the previous [multi-step GraphQL tutorial](../multi-step/explore-graphql-api.md), you explored the GraphiQL Integrated Development Environment (IDE) where you tested and refined some common GraphQL queries. In this chapter, you will use the GraphiQL IDE to explore more advanced queries to gather data of the Content Fragments that you created in the previous chapter.

## Prerequisites {#prerequisites}

This document is part of a multi-part tutorial. Please ensure that the previous chapters have been completed before proceeding with this chapter.

The GraphiQL IDE must be installed before completing this chapter. Please follow the installation instructions in the previous [multi-step GraphQL tutorial](../multi-step/explore-graphql-api.md) for more information.

## Objectives {#objectives}

In this chapter, you will learn how to:

* Filter a list of Content Fragments with references using query variables
* Filter for content within a fragment reference
* Query for inline content and fragment references from a multi-line text field
* Query using directives
* Query for the JSON Object content type

## Filter a list of Content Fragments using query variables

In the previous [multi-step GraphQL tutorial](../multi-step/explore-graphql-api.md), you learned how to filter a list of Content Fragments. Here, you will expand this knowledge and filter using variables. 

When developing client applications, in most cases you will need to filter Content Fragments based on dynamic arguments. The AEM GraphQL API allows you to pass these arguments as variables in a query in order to avoid string construction on the client side at runtime. For more information on GraphQL variables, see the [GraphQL documentation](https://graphql.org/learn/queries/#variables).

For this example, query all Instructors that have a particular skill.

1. In the GraphiQL IDE, paste the following query into the left panel:

    ```graphql
    query listPersonBySkill ($skillFilter: String!){
      personList(
        _locale: "en"
        filter: {skills: {_expressions: [{value: $skillFilter}]}}
      ) {
        items {
          fullName
          contactInfo {
            phone
            email
          }
          profilePicture {
            ... on ImageRef {
              _path
            }
          }
          biography {
            plaintext
          }
          instructorExperienceLevel
          skills
        }
      }
    }
    ```

    The `listPersonBySkill` query above accepts one variable (`skillFilter`) that is a required `String`. This query performs a search against all Person Content Fragments and filters them based on the `skills` field and the string that is passed in `skillFilter`.

    Note that `listPersonBySkill` includes the `contactInfo` property, which is a fragment reference to the Contact Info model defined in the previous chapters. The Contact Info model contains `phone` and `email` fields. You must include at least one of these fields in the query for it to perform correctly.

    ```graphql
    contactInfo {
            phone
            email
          }
    ```

1. Next, let's define `skillFilter` and get all Instructors that are proficient in skiing. Paste the following JSON string in the Query Variables panel in the GraphiQL IDE:

    ```json
    {
	    "skillFilter": "Skiing"
    }
    ```

1. Execute the query. The result should look similar to the following:

    ```json
    {
      "data": {
        "personList": {
          "items": [
            {
              "fullName": "Stacey Roswells",
              "contactInfo": {
                "phone": "209-888-0011",
                "email": "sroswells@wknd.com"
              },
              "profilePicture": {
                "_path": "/content/dam/wknd/en/contributors/stacey-roswells.jpg"
              },
              "biography": {
                "plaintext": "Stacey Roswells is an accomplished rock climber and alpine adventurer.\nBorn in Baltimore, Maryland, Stacey is the youngest of six children. Her father was a lieutenant colonel in the US Navy and her mother was a modern dance instructor. Her family moved frequently with her father’s duty assignments, and she took her first pictures when he was stationed in Thailand. This is also where Stacey learned to rock climb."
              },
              "instructorExperienceLevel": "Advanced",
              "skills": [
                "Rock Climbing",
                "Skiing",
                "Backpacking"
              ]
            }
          ]
        }
      }
    }
    ```

## Filter for content within a fragment reference

The AEM GraphQL API allows you to query nested Content Fragments. In the previous chapter, you added three new fragment references to an Adventure Content Fragment: `location`, `instructorTeam`, and `administrator`. Now, let's filter all Adventures for any Administrator that has a particular name.

>[!CAUTION]
>
>Only one model must be allowed as reference for this query to perform correctly.

1. In the GraphiQL IDE, paste the following query into the left panel:

    ```graphql
    query getAdventureAdministratorDetailsByAdministratorName ($name: String!){
      adventureList(
      _locale: "en"
        filter: {administrator: {fullName: {_expressions: [{value: $name}]}}}
      ) {
        items {
          adventureTitle
          administrator {
            fullName
            contactInfo {
              phone
              email
            }
            administratorDetails {
              json
            }
          }
        }
      }
    }
    ```

1. Next, paste the following JSON string in the Query Variables panel:

    ```json
    {
	    "name": "Jacob Wester"
    }
    ```

    The `getAdventureAdministratorDetailsByAdministratorName` query filters all Adventures for any `administrator` of `fullName` "Jacob Wester", returning information from across two nested Content Fragments: Adventure and Instructor.

1. Execute the query. The result should look similar to the following:

    ```json
    {
      "data": {
        "adventureList": {
          "items": [
            {
              "adventureTitle": "Yosemite Backpacking",
              "administrator": {
                "fullName": "Jacob Wester",
                "contactInfo": {
                  "phone": "209-888-0000",
                  "email": "jwester@wknd.com"
                },
                "administratorDetails": {
                  "json": [
                    {
                      "nodeType": "paragraph",
                      "content": [
                        {
                          "nodeType": "text",
                          "value": "Jacob Wester has been coordinating backpacking adventures for 3 years."
                        }
                      ]
                    }
                  ]
                }
              }
            }
          ]
        }
      }
    }
    ```

## Query for inline references from a multi-line text field {#query-rte-reference}

The AEM GraphQL API allows you to query for content and fragment references within multi-line text fields. In the previous chapter, you added both reference types into the **Description** field of the Yosemite Team Content Fragment. Now, let's retrieve these references.

1. In the GraphiQL IDE, paste the following query into the left panel:

    ```graphql
    query getTeamByAdventurePath ($fragmentPath: String!){
      adventureByPath (_path: $fragmentPath) {
        item {
          instructorTeam {
            _metadata {
              stringMetadata {
                name
                value
              }
          }
            teamFoundingDate
            description {
              plaintext
            }
          }
        }
        _references {
          ... on ImageRef {
            __typename
            _path
          }
          ... on LocationModel {
            __typename
            _path
            name
            address {
              streetAddress
              city
              zipCode
              country
            }
            contactInfo {
              phone
              email
            }
          }
        }
      }
    }
    ```

    The `getTeamByAdventurePath` query filters all Adventures by path and returns data for the `instructorTeam` fragment reference of a specific Adventure.

    `_references` is a system-generated field that is used to reveal references, including those that are inserted into multi-line text fields. 
    
    The `getTeamByAdventurePath` query retrieves multiple references. First, it uses the built-in `ImageRef` object to retrieve the `_path` and `__typename` of images inserted as content references into the multi-line text field. Next, it uses `LocationModel` to retrieve the data of the Location Content Fragment inserted into the same field.

    Note that the query also includes the `_metadata` field. This allows you to retrieve the name of the Team Content Fragment and display it later in the WKND app.

1. Next, paste the following JSON string in the Query Variables panel to get the Yosemite Backpacking Adventure:

    ```json
    {
	    "fragmentPath": "/content/dam/wknd/en/adventures/yosemite-backpacking/yosemite-backpacking"
    }
    ```

1. Execute the query. The result should look similar to the following:

    ```json
    {
      "data": {
        "adventureByPath": {
          "item": {
            "instructorTeam": {
              "_metadata": {
                "stringMetadata": [
                  {
                    "name": "title",
                    "value": "Yosemite Team"
                  },
                  {
                    "name": "description",
                    "value": ""
                  }
                ]
              },
              "teamFoundingDate": "2016-05-24",
              "description": {
                "plaintext": "\n\nThe team of professional adventurers and hiking instructors working in Yosemite National Park.\n\nYosemite Valley Lodge"
              }
            }
          },
          "_references": [
            {
              "__typename": "LocationModel",
              "_path": "/content/dam/wknd/en/adventures/locations/yosemite-valley-lodge/yosemite-valley-lodge",
              "name": "Yosemite Valley Lodge",
              "address": {
                "streetAddress": "9006 Yosemite Lodge Drive",
                "city": "Yosemite National Park",
                "zipCode": "95389",
                "country": "United States"
              },
              "contactInfo": {
                "phone": "209-992-0000",
                "email": "yosemitelodge@wknd.com"
              }
            },
            {
              "__typename": "ImageRef",
              "_path": "/content/dam/wknd/en/adventures/teams/yosemite-team/team-yosemite-logo.png"
            }
          ]
        }
      }
    }
    ```

    Note that the `_references` field reveals both the logo image and the Yosemite Valley Lodge Content Fragment that was inserted into the **Description** field.


## Query using directives

Sometimes when developing client applications, you need to conditionally change the structure of your queries. In this case, the AEM GraphQL API allows you to use GraphQL directives in order to change the behavior of your queries based on the provided criteria. For more information on GraphQL directives, see the [GraphQL documentation](https://graphql.org/learn/queries/#directives).

In the [previous section](#query-rte-reference), you learned how to query for inline references within multi-line text fields. Note that the content was retrieved from the `description` filed in the `plaintext` format. Next, let's expand that query and use a directive to conditionally retrieve `description` in the `json` format as well.

1. In the GraphiQL IDE, paste the following query into the left panel:

    ```graphql
    query getTeamByAdventurePath ($fragmentPath: String!, $includeJson: Boolean!){
      adventureByPath(_path: $fragmentPath) {
        item {
          instructorTeam {
            _metadata{
              stringMetadata{
                name
                value
              }
            }
            teamFoundingDate
            description {
              plaintext
              json @include(if: $includeJson)
            }
          }
        }
        _references {
          ... on ImageRef {
            __typename
            _path
          }
          ... on LocationModel {
            __typename
            _path
            name
            address {
              streetAddress
              city
              zipCode
              country
            }
            contactInfo {
              phone
              email
            }
          }
        }
      }
    }
    ```
    
    The query above accepts one more variable (`includeJson`) that is a required `Boolean`, also known as the query's directive. A directive can be used to conditionally include data from the `description` field in the `json` format based on the boolean that is passed in `includeJson`.

1. Next, paste the following JSON string in the Query Variables panel:

    ```json
    {
      "fragmentPath": "/content/dam/wknd/en/adventures/yosemite-backpacking/yosemite-backpacking",
      "includeJson": false
    }
    ```

1. Execute the query. You should get the same result as in the previous section on [how to query for inline references within multi-line text fields](#query-rte-reference). 

1. Update the `includeJson` directive to `true` and execute the query again. The result should look similar to the following:

    ```json
    {
      "data": {
        "adventureByPath": {
          "item": {
            "instructorTeam": {
              "_metadata": {
                "stringMetadata": [
                  {
                    "name": "title",
                    "value": "Yosemite Team"
                  },
                  {
                    "name": "description",
                    "value": ""
                  }
                ]
              },
              "teamFoundingDate": "2016-05-24",
              "description": {
                "plaintext": "\n\nThe team of professional adventurers and hiking instructors working in Yosemite National Park.\n\nYosemite Valley Lodge",
                "json": [
                  {
                    "nodeType": "paragraph",
                    "content": [
                      {
                        "nodeType": "reference",
                        "data": {
                          "path": "/content/dam/wknd/en/adventures/teams/yosemite-team/team-yosemite-logo.png",
                          "mimetype": "image/png"
                        }
                      }
                    ]
                  },
                  {
                    "nodeType": "paragraph",
                    "content": [
                      {
                        "nodeType": "text",
                        "value": "The team of professional adventurers and hiking instructors working in Yosemite National Park."
                      }
                    ]
                  },
                  {
                    "nodeType": "paragraph",
                    "content": [
                      {
                        "nodeType": "reference",
                        "data": {
                          "href": "/content/dam/wknd/en/adventures/locations/yosemite-valley-lodge/yosemite-valley-lodge",
                          "type": "fragment"
                        },
                        "value": "Yosemite Valley Lodge"
                      }
                    ]
                  }
                ]
              }
            }
          },
          "_references": [
            {
              "__typename": "LocationModel",
              "_path": "/content/dam/wknd/en/adventures/locations/yosemite-valley-lodge/yosemite-valley-lodge",
              "name": "Yosemite Valley Lodge",
              "address": {
                "streetAddress": "9006 Yosemite Lodge Drive",
                "city": "Yosemite National Park",
                "zipCode": "95389",
                "country": "United States"
              },
              "contactInfo": {
                "phone": "209-992-0000",
                "email": "yosemitelodge@wknd.com"
              }
            },
            {
              "__typename": "ImageRef",
              "_path": "/content/dam/wknd/en/adventures/teams/yosemite-team/team-yosemite-logo.png"
            }
          ]
        }
      }
    }
    ```

## Query for the JSON Object content type

Remember that in the previous chapter on authoring Content Fragments, you added a JSON object into the **Weather by Season** field. Let's now retrieve that data within the Location Content Fragment.

1. In the GraphiQL IDE, paste the following query into the left panel:

    ```graphql
    query getLocationDetailsByLocationPath ($fragmentPath: String!) {
      locationByPath(_path: $fragmentPath) {
        item {
          name
          description {
            json
          }
          contactInfo {
            phone
            email
          }
          locationImage {
            ... on ImageRef {
              _path
            }
          }
          weatherBySeason
          address {
            streetAddress
            city
            state
            zipCode
            country
          }
        }
      }
    }
    ```

1. Next, paste the following JSON string in the Query Variables panel:

    ```json
    {
      "fragmentPath": "/content/dam/wknd/en/adventures/locations/yosemite-national-park/yosemite-national-park"
    }
    ```

1. Execute the query. The result should look similar to the following:

    ```json
    {
      "data": {
        "locationByPath": {
          "item": {
            "name": "Yosemite National Park",
            "description": {
              "json": [
                {
                  "nodeType": "paragraph",
                  "content": [
                    {
                      "nodeType": "text",
                      "value": "Yosemite National Park is in California’s Sierra Nevada mountains. It’s famous for its gorgeous waterfalls, giant sequoia trees, and iconic views of El Capitan and Half Dome cliffs."
                    }
                  ]
                },
                {
                  "nodeType": "paragraph",
                  "content": [
                    {
                      "nodeType": "text",
                      "value": "Hiking and camping are the best ways to experience Yosemite. Numerous trails provide endless opportunities for adventure and exploration."
                    }
                  ]
                }
              ]
            },
            "contactInfo": {
              "phone": "209-999-0000",
              "email": "yosemite@wknd.com"
            },
            "locationImage": {
              "_path": "/content/dam/wknd/en/adventures/locations/yosemite-national-park/yosemite-national-park.jpeg"
            },
            "weatherBySeason": {
              "summer": "81 / 89°F",
              "fall": "56 / 83°F",
              "winter": "46 / 51°F",
              "spring": "57 / 71°F"
            },
            "address": {
              "streetAddress": "9010 Curry Village Drive",
              "city": "Yosemite Valley",
              "state": "CA",
              "zipCode": "95389",
              "country": "United States"
            }
          }
        }
      }
    }
    ```

    Note that the `weatherBySeason` field contains the JSON object added in the previous chapter.

## Query for all content at once

So far, multiple queries have been executed to illustrate the capabilities of the AEM GraphQL API. The same data could be retrieved with only a single query:

```graphql
query getAllAdventureDetails($fragmentPath: String!) {
  adventureByPath(_path: $fragmentPath){
    item {
      _path
      adventureTitle
      adventureActivity
      adventureType
      adventurePrice
      adventureTripLength
      adventureGroupSize
      adventureDifficulty
      adventurePrice
      adventurePrimaryImage{
        ...on ImageRef{
          _path
          mimeType
          width
          height
        }
      }
      adventureDescription {
        html
        json
      }
      adventureItinerary {
        html
        json
      }
      location {
        _path
        name
        description {
          html
          json
        }
        contactInfo{
          phone
          email
        }
        locationImage{
          ...on ImageRef{
            _path
          }
        }
        weatherBySeason
        address{
            streetAddress
            city
            state
            zipCode
            country
        }
      }
      instructorTeam {
        _metadata{
            stringMetadata{
                name
                value
            }
        }        
        teamFoundingDate
        description {
            json
        }
        teamMembers {
            fullName
            contactInfo {
                phone
                email
            }
            profilePicture{
                ...on ImageRef {
                    _path
                }
            }
            instructorExperienceLevel
            skills
            biography {
                html
            }
        }       
     }
      administrator {
            fullName
            contactInfo {
                phone
                email
            }
            biography {
                html
            }
        }
    }
    _references {
        ...on ImageRef {
            _path
        mimeType
        }
        ...on LocationModel {
            _path
                __typename
        }
    }
  }
}

# in Query Variables
{
  "fragmentPath": "/content/dam/wknd/en/adventures/yosemite-backpacking/yosemite-backpacking"
}
```

## Additional queries for the WKND app

The following queries are listed to retrieve all the data needed in the WKND app. These queries do not demonstrate any new concepts and are only provided as a reference to help you build your implementation.

1. **Get team members for a specific Adventure**:

    ```graphql
    query getTeamMembersByAdventurePath ($fragmentPath: String!){
      adventureByPath (_path: $fragmentPath ) {
        item {
          instructorTeam {
            teamMembers{
              fullName
              contactInfo{
                phone
                email
              }
            profilePicture {
                ... on ImageRef {
                  _path
                }
            }
              instructorExperienceLevel
              skills
              biography{
                plaintext
              }
            }
          }
        }
      }
    }

    # in Query Variables
    {
      "fragmentPath": "/content/dam/wknd/en/adventures/yosemite-backpacking/yosemite-backpacking"
    }
    ```

1. **Get Location path for a specific Adventure**

    ```graphql
    query getLocationPathByAdventurePath ($fragmentPath: String!){
      adventureByPath (_path: $fragmentPath){
        item {
          location{
            _path  
          } 
        }
      }
    }

    # in Query Variables
    {
      "fragmentPath": "/content/dam/wknd/en/adventures/yosemite-backpacking/yosemite-backpacking"
    }
    ```

1. **Get the team location by its path**

    ```graphql
    query getTeamLocationByLocationPath ($fragmentPath: String!){
      locationByPath (_path: $fragmentPath) {
        item {
          name
          description{
            json
          }
          contactInfo{
            phone
            email
          }
            address{
            streetAddress
            city
            state
            zipCode
            country
          }
        }
      }
    }

    # in Query Variables
    {
      "fragmentPath": "/content/dam/wknd/en/adventures/locations/yosemite-valley-lodge/yosemite-valley-lodge"
    }
    ```

## Congratulations!

Congratulations! You have now tested advanced queries to gather data of the Content Fragments that you created in the previous chapter.

## Next steps

In the [next chapter](/help/headless-tutorial/graphql/advanced-graphql/graphql-persisted-queries.md), you will learn how to persist GraphQL queries and why it is best practice to use persisted queries in your applications.
