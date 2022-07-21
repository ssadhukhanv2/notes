* [in28minute course](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-step-by-step/learn/lecture/23003296#overview)

# **AWS Certified Developer Associate**


* [Explain the advantages and disadvantages of using cloud](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-step-by-step/learn/lecture/23000460#overview)

* **Challenges without Cloud**: 
    * To support surge in application application usage capacity planning needs to be done in advance. For example- For a online shopping application, if there is a peak usage during holidays and weekends and less load during other time, we need to buy the full infrastructure to support peak usage.
    * This leads to low infrastructure utilization when there is low usage.
    * Buying the hardware leads to high cost of procuring the infrastructure.
    * Needs a dedicated team support the maintenence of the hardware.

* **Advantages of using Cloud**:
    * Cloud allows on demand resource provisioning, which means we can buy addional resources just for the duration of peak usage and release it back when the usage is low.
    * This usually leads to low cost, less upfront planning & avoid undifferentiated heavy lifting.
    * Undifferentiated heavy lifting refers to additional IT work that companies do but doesn't add value to the mission of the company. For example-maintain a database, upgrade firewall etc. This is automatically managed by the cloud provider so that Companies can focus on the business side of things that actually add value.

* **Challeges to use Cloud:**
    
    * Building Cloud Enabled application may be complex.



## **Regions || Availability Zone || Edge Locations**

* [Explain the difference between Regions & Availability Zone](https://tcsglobal.udemy.com/course/aws-certified-developer-associate-dva-c01/learn/lecture/26100712#overview)

* **Region:** Regions are basically **``cluster of data centers``**. There are multiple AWS Regions around the world. Example: ``us-east-2, us-east-1, ap-east-1, ap-southeast-2`` etc
    * Most AWS Services are scoped to a single region.
    * Considerations while choosing an AWS region to launch a service:
        * **``Compliance:``** We may have legal requirement of keeping data within a specfic country, in such a scenario we need to launch the service in the Region specific to the corresponding country.
        * **``Proximity:``** We may need to choose a region that is close to the end user. This reduces the latency.
        * **``Available Services:``** Not all services are available in all regions so may need to choose a region where a specific service is available incase we need to use them.
        * **``Pricing:``** Pricing may vary from region to region, so we may need to consider that while choosing the regions.

* **Availablility Zones:** Each AWS region is composed of multiple availablity zones(Min 2, Max 6). Example: ``ap-southeast-2a``, ``ap-southeast-2b``, ``ap-southeast-2c``
    * Each AZ is **``one or more discrete data centers``** with redundant power, networking and connectivity.
    * They are interconnected by high bandwidth ultra low latency networking.
    * They are separate from each other, so they are isolated from disaster.

* **Edge Locations:** Amazon has 216 point of presence(205 Edge Locations & 11 Regional Caches across 42 countries around the world)
    * This allows content to be delivered to end users with ultra low latency.