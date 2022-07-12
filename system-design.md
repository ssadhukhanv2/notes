# [System Design](https://completedesigninterviewcourse.com/system-design-interview/)

* Explain **SOLID** Principles
[Part 1](https://www.youtube.com/watch?v=oRA-xnqlB10) 
[Part 2](https://www.youtube.com/watch?v=zn2Sn7lMnLM) 


* [Explain different **Response Codes**](https://medium.com/geekculture/http-response-codes-for-crud-eabdda3ed617)
* **``200 Success``** Used to denote a successful scenario, where the requester expects the API to return some data and the api has located/constructed the data as the body of the reponse. 
* **``201 Created``** Appropriate where new resource is being created
* **``202 Accepted``** Used to signify users request has been received how ever the reponse is not the expected response of the requester. It only signifies that the processing of the data has started.
* **``204 No Content``** Indicates that the request was successful but there was no data sent in the reponse. Of used when a resource is deleted or no data is found.
* **``206 Partial Content``** Generally returned by a read operation when the size of the response is to big to be fit in a single reponse. Often signifies that paging has been implemented.
* **``400 Bad Request``** API has trouble parsing the request or the request was malformed in some way.
* **``403 Forbidden``** When appropriate authorization 
*  **``404 Not Found``** Unable to locate the Resource ID passed to the API
information has not been supplied. 
* **``405 Not Allowed``** HTTP method was inappropriate for this endpoint. For example client used GET on a POST endpoint.
* **``500 Internal Server Error``** Lets the client know that the API encountered some error and thus API owner should be contacted.
* **``501 Not Implemented``** Often signifies that the API would be introduced later but not implemented now.



* [How will you design the **database for the below requirements**](https://youtu.be/P_eh1b6vE-4?t=170)
  * User should be able to **view/edit his profile** containing the below information.
  * On the top left we should **show user Profile Phono**
  * On the top right **name and contact number** should be displayed
  * User can **enter multiple skills** & as the user types, **autosuggest the skills**
  * User may choose to enter **Educational information**
  * User may chooose to **enter details about his previous and current employers**
  * User may **give or receive recommendation** from Collegues
  * User may send **connection requests** to other users. Unless the user approves the connection request, the sender will just be a follower. Once the connection request is approved, both the sender & receipient becomes follower of each other.


* [How will you design an **URL shortening service**](https://tcsglobal.udemy.com/course/system-design-interview-prep/learn/lecture/28976014#reviews)
* [How will you **design a DataLake** of Big Data application](https://tcsglobal.udemy.com/course/system-design-interview-prep/learn/lecture/28975340#reviews) **S3** to dump data, **Amazon Glue** to throw a structure on it, **Amazon Athena** Query the data, **Partition** the data based on access pattern)
* [Sharding, How to design a **scalable mongodb database**, How will you handle Normalization](https://tcsglobal.udemy.com/course/system-design-interview-prep/learn/lecture/28975322#reviews)
* [How to implement **Pilot Light** vs **Warm Standby**  Disaster Recovery/Failover in **AWS**](https://aws.amazon.com/blogs/architecture/disaster-recovery-dr-architecture-on-aws-part-iii-pilot-light-and-warm-standby/)
* [Failover Strategies](https://tcsglobal.udemy.com/course/system-design-interview-prep/learn/lecture/28975314#reviews): Cold StandBy, Warm Standby, Hot Standby