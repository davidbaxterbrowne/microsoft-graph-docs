# Archive team

> **Important:** APIs under the /beta version in Microsoft Graph are in preview and are subject to change. Use of these APIs in production applications is not supported.

Archive the specified Microsoft Teams team. 
An archived team prevents all users from sending or liking messages on any channel in the team, from editing the team's name, description, and other settings, and in general from most changes to the team. 
Membership changes to the team continue to be allowed.

Archiving is an async operation. A team is archived once the async operation completes successfully, which may occur subsequent to a response from this API.

To restore a team from its archived state, use the API to [unarchive](team_unarchive.md).

## Permissions
One of the following permissions is required to call this API. To learn more, including how to choose permissions, see [Permissions](../../../concepts/permissions_reference.md).

|Permission type      | Permissions (from least to most privileged)              |
|:--------------------|:---------------------------------------------------------|
|Delegated (work or school account) | Group.ReadWrite.All    |
|Delegated (personal Microsoft account) | Not supported.    |
|Application | Not supported. |

## HTTP request
<!-- { "blockType": "ignored" } -->
```http
POST /groups/{id}/team/archive
```
## Request headers
| Header       | Value |
|:---------------|:--------|
| Authorization  | Bearer {token}. Required.  |

## Request body
In the request, you may _optionally_ include the `shouldSetSpoSiteReadOnlyForMembers` parameter in a JSON body, as follows.
```JSON
{
    "shouldSetSpoSiteReadOnlyForMembers": true
}
```
This optional parameter defines whether to set permissions for team members to read-only on the Sharepoint Online site associated with the team. Setting it to false or omitting the body altogether will result in this step being skipped.

## Response

If archiving is started successfully, this method returns a `202 Accepted` response code. The response will also contain a `Location` header, which contains the location of the [teamsAsyncOperation](..\resources\teamsAsyncOperation.md) that was created to handle archiving of the team. Check the status of the archiving operation by making a GET request to this location.

## Example
#### Request
The following is an example of a request.
<!-- {
  "blockType": "ignored",
  "name": "archive_team"
}-->
```http
POST https://graph.microsoft.com/beta/groups/{id}/team/archive
```
#### Response
The following is an example of a response.
```http
HTTP/1.1 202 Accepted
Location: /groups({id})/team/operations({opId})
Content-Type: text/plain
Content-Length: 0
```
<!-- uuid: e848414b-4669-4484-ac36-1504c58a3fb8
2015-10-25 14:57:30 UTC -->
<!-- {
  "type": "#page.annotation",
  "description": "Archive team",
  "keywords": "",
  "section": "documentation",
  "tocPath": ""
}-->