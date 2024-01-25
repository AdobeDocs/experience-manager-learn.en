---
title: Save and retrieve draft letters
description: Learn how to save and retrieve draft letters
feature: Interactive Communication
doc-type: article
version: 6.5
topic: Development
role: Developer
level: Intermediate
jira: KT-10208
exl-id: dc6f64a0-7059-4392-9c29-e66bdef4fd4d
duration: 103
---
# Save and retrieve draft letters

The following code is used to save the letter instance. The metadata of the letter instance is stored in the _icdrafts_ table. A unique string(draftID) is generated and returned. This unique string is then used to retrieve saved letter instance.

```java
public String save(CCRDocumentInstance letterToSave) throws CCRDocumentException {
  String insertRowSQL = "INSERT INTO aemformstutorial.icdrafts(draftID,documentID,status,owner,name) VALUES(?,?,?,?,?)";
  log.debug(" in save IC Draft" + letterToSave.getDocumentId() + letterToSave.getName());
  UUID uuid = UUID.randomUUID();
  String uuidString = uuid.toString();
  Connection connection = getConnection();
  PreparedStatement pstmt = null;
  Document icData = letterToSave.getData();
  try {
    pstmt = connection.prepareStatement(insertRowSQL);
    pstmt.setString(1, uuidString);
    pstmt.setString(2, letterToSave.getDocumentId());
    pstmt.setString(3, "DRAFT");
    pstmt.setString(4, letterToSave.getCreatedBy());
    pstmt.setString(5, letterToSave.getName());
    icData.copyToFile(new File(uuidString + ".xml"));
    log.debug("Executing the insert statment  " + pstmt.executeUpdate());
    connection.commit();
  } catch (IOException | SQLException e) {
    log.debug("The error is " + e.getMessage());
  } finally {
    if (pstmt != null) {
      try {
        pstmt.close();
      } catch (SQLException e) {
        log.debug("Error in closing prepared statment" + e.getMessage());
      }
    }
    if (connection != null) {
      try {
        log.debug("Closing the connection in Save Letter Draft");
        connection.close();
      } catch (SQLException e) {
        log.debug("Error in closing connection" + e.getMessage());
      }
    }

  }

  return uuidString;
}
```

## Get Letter

The following code was written to fetch the saved draft letter.
To load a saved letter instances you need to provide the draftID. Based on this draftID we query the database to get the addtional metadata about the letter. The same draftID is used to create the letter's data by reading the appropriate xml from the file system. A CCRDocumentInstance object is then constructed and returned.


```java
@Override
public CCRDocumentInstance get(String draftID) throws CCRDocumentException {

  String selectStatement = "Select documentID from aemformstutorial.icdrafts where draftID='" + draftID + "'";
  log.debug("The select statement is " + selectStatement);
  Connection connection = getConnection();
  Statement statement = null;
  String documentID = "";
  try {
    statement = connection.createStatement();
    ResultSet rs = statement.executeQuery(selectStatement);
    while (rs.next()) {
      documentID = rs.getString("documentID");

    }
  } catch (SQLException e) {
    log.debug("The error is " + e.getMessage());
  }
  Document draftData = new Document(new File(draftID + ".xml"));
  CCRDocumentInstance draftInstance = new CCRDocumentInstance(draftData, "abc", documentID, CCRDocumentInstance.Status.DRAFT);
  draftInstance.setId(draftID);
  return draftInstance;
}
```

### Update Letter

The following code was used to update saved letter instance. The updated letter's data is written to the file system using the letter id.

```java
public void update(CCRDocumentInstance letterInstanceToUpdate) throws CCRDocumentException {
        Document icData = letterInstanceToUpdate.getData();
        String draftID = letterInstanceToUpdate.getId();
        log.debug("updating letter instance with draft id =  "+draftID);
        try
            {
                icData.copyToFile(new File(draftID+".xml"));
            } 
        catch (IOException e)
            {
                log.debug("Error updating "+e.getMessage());;
            }
        
    }
```

### Get All Saved Letters

AEM Forms does not provide any out of the box user interaface to list the saved letters. For this article I list the saved letter instances in a tabular format using an adaptive form.
You can customize the query to fetch the saved letter instances. In this example, I am querying for saved letter instance by "admin".

```java
    public List < CCRDocumentInstance > getAll(String arg0, Date arg1, Date arg2, Map < String, Object > arg3) throws CCRDocumentException {
      String selectStatement = "Select * from aemformstutorial.icdrafts where owner = 'admin'";
      Connection connection = getConnection();
      Statement statement = null;
      String documentID = "";
      List < CCRDocumentInstance > listOfDrafts = new ArrayList < CCRDocumentInstance > ();
      String draftID;
      String savedInstanceName = "";
      try {
        statement = connection.createStatement();
        ResultSet rs = statement.executeQuery(selectStatement);
        while (rs.next()) {
          documentID = rs.getString("documentID");
          draftID = rs.getString("draftID");
          savedInstanceName = rs.getString("name");
          Document draftData = new Document(new File(draftID + ".xml"));
          CCRDocumentInstance draftLetter = new CCRDocumentInstance(draftData, savedInstanceName, documentID, CCRDocumentInstance.Status.DRAFT);
          listOfDrafts.add(draftLetter);
        }
      } catch (SQLException e) {
        log.debug("The error is " + e.getMessage());
      } finally {
        if (statement != null) {
          try {
            statement.close();
          } catch (SQLException e) {
            log.debug("error in closing statement" + e.getMessage());
          }
        }
        if (connection != null) {
          try {
            connection.close();
          } catch (SQLException e) {
            log.debug("error in closing connection" + e.getMessage());
          }
        }
      }

      return listOfDrafts;
    }
```

### Eclipse Project

The eclipse project with sample implementation can be [downloaded from here](assets/icdrafts-eclipse-project.zip)
