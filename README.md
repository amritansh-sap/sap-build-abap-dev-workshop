# Hands-On Guide: Integrating ABAP with SAP Build

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Environment Setup](#environment-setup)
4. [Hands-On Exercises](#hands-on-exercises)
5. [Key Takeaways](#key-takeaways)
6. [Troubleshooting](#troubleshooting)
7. [Appendix](#appendix)

## Introduction

Welcome to this hands-on session on integrating ABAP with SAP Build. This guide will walk you through step-by-step instructions to understand and implement the integration effectively.

**Objectives:**

- Understand the role of SAP Build in ABAP development.
- Set up the environment for integration.
- Create and extend ABAP packages via SAP Build.

## Prerequisites

**Knowledge Requirements:** Familiarity with SAP Build, ABAP, and SAP BTP.

**Access Requirements:** Ensure access to the following:

- SAP BTP Account with necessary entitlements.
- SAP Build subscription.
- ABAP system (BTP or S/4HANA Public Cloud).

**Tools:**

- [Eclipse](https://www.eclipse.org/downloads/packages/release/2024-12/m3) with ADT installed ([Download ADT](https://tools.hana.ondemand.com/latest)). Additional help guide [here](./ADTSetup.md).
- Updated browser supporting SAP Build UI.

## Environment Setup

<!-- Note: Can be skipped

**Step 1: Subscribing to SAP Build**

1. Log into your SAP BTP Cockpit.
2. Navigate to Subscriptions and select SAP Build.
3. Follow the steps to activate the subscription.

**Step 2: Setting Up Destinations**

1. Navigate to Connectivity > Destinations in SAP BTP.
2. Create a destination with the following properties:

- Name: ABAP_System
- Type: HTTP
- URL: <Your ABAP System URL>
- Authentication: SAMLAssertion

3. Test the connection to ensure it's active.

**Step 3: Configuring Communication Systems**

1. Download your BTP subaccount's trust certificate.
2. Configure the communication system in the ABAP environment using the Communication Systems app. -->

**SAP Build system with access to Build Code, Build Apps and Build Process Automation is already available:** [Link](https://spa-us10-nwjsondh.us10.build.cloud.sap)

## Hands-On Exercises

**Note:** The system is for testing purposes only. After the session, all data will be lost, so keep that in mind when creating new TRs or objects.

### Exercise 1: Creating an ABAP Project in SAP Build

1. **Access the SAP Build Lobby:**

   Log in to the [SAP Build Lobby](https://spa-us10-nwjsondh.us10.build.cloud.sap) and click `Create` > `Build an Application` > `ABAP Cloud`.

   ![image](./assets/project-1.png)

   ![image](./assets/project-2.png)

   ![image](./assets/project-3.png)

2. **Select System:**

   From the System dropdown, select **BD2**, which is the mapped system for the session. This system has been pre-configured for the session.

3. **Package Selection:**

   You can either use the existing packages per user : `ZTESTER01`, `ZTESTER02` … or create a new package under these as super packages. Ensure that the new package name starts with **Z**.

   **A. Working with an Existing Package:**

   ![image](./assets/project-4.png)

   **B. Working with a New Package:**

   i. Create a new Package by providing the super package name, package name and description.![image](./assets/project-5.png)
   ii. Configuring Transport Requests
   a. Use Existing Transport Request: Select an existing transport request (TR) from the dropdown.
   ![image](./assets/project-6.png)
   b. Or Create a New Transport Request: create a new transport request by entering a description.

4. **Proceed to ABAP Project Creation:**

   ![image](./assets/project-7.png)

5. **Post successful creation open the project in Eclipse.**

   i. Allow browser to open eclipse. ![image](./assets/project-8.png)

   ii. Create a new project from the link. ![image](./assets/project-9.png)

   iii. Click on Next. ![image](./assets/project-10.png)

   iv. Logon using test user through browser and close the new tab once done. ![image](./assets/project-11.png) ![image](./assets/project-12.png)

   v. Finish with the creation ![image](./assets/project-13.png)

### Exercise 2: Generating and Using Service Bindings

1. **Create a New ABAP Object:** Use the Repository Object Generator Wizard to create a new OData UI service for your ABAP object.

   i. Browse existing objects.![image](./assets/fiori-1.png)

   ii. Search for “ZTRAVEL” and then chose the object accordingly as per your user, example for Tester01 select ZTRAVEL01 and press OK.![image](./assets/fiori-2.png)

   iii. Press Next.![image](./assets/fiori-3.png)

   iv. Once the packages are validated press Next on the screen.

   v. Validate the general details and press Next again.

   vi. Review the list of repository objects that are going to be generated and press Next again.

   vii. Select a transport request from the list or browse for existing requests from under the “Enter a request number” and select the “CEI Workshop" request. You can also create a new request.

   viii. Click Finish and wait for artifacts to generate.

   ix. Publish the artifacts.![image](./assets/fiori-7a.png)

   x. Preview the Fiori Application.![image](./assets/fiori-7b.png)

2. **Create a Fiori Project:** Link Business Application Studio to your project

   i. Create a Fiori dev space for yourself [here](https://spa-us10-nwjsondh.us10cf.applicationstudio.cloud.sap/index.html?externalRedirect=true).![image](./assets/fiori-4.png)

   ii. You would need the dev space id of the newly created dev space to complete the next steps.![image](./assets/fiori-5.png)

   iii. Go back to eclipse and open project properties.![image](./assets/fiori-6.png)

   iv. Use the below details and link the dev space under “ABAP Development Tools” -> “External IDE Configuration” -> “Configure External IDE” -> “SAP Business Application Studio”

   - URL: <https://spa-us10-nwjsondh.us10cf.applicationstudio.cloud.sap/index.html>
   - Dev Space Id: `<dev space id from previous step>`
   - Destination Name: `BD2`

   v. Click on Apply and Close.

   vi. Select the newly published entity and select Create Fiori Project.![image](./assets/fiori-7b.png)

   vii. Select the “List Report Page” as the template.![image](./assets/fiori-8.png)

   viii. Review the Entity Selection step and press Next.

   ix. Review the project attributes and press Finish. This will generate a Fiori Application. Please wait for the files to be load.

   x. Click on Preview application and select start-mock. This will setup the dependencies and start a mock application.![image](./assets/fiori-9.png)![image](./assets/fiori-10.png)

   xi. In the preview app press Go to view mock data.![image](./assets/fiori-11.png)

## Key Takeaways

- SAP Build simplifies ABAP extensibility.
- Integration allows seamless development across SAP BTP and S/4HANA.
- Service bindings can be reused across multiple SAP Build tools, enhancing collaboration and flexibility.

## Troubleshooting

### Common Issues

| Issue                        | Possible Solution                                         |
| ---------------------------- | --------------------------------------------------------- |
| Destination not reachable    | Verify URL and authentication settings.                   |
| Transport request not listed | Check ABAP system connection and permissions.             |
| Service binding not found    | Ensure the package is created in the correct ABAP system. |

## Appendix

### References

- SAP Build Documentation
- SAP BTP ABAP Environment Guide

### Glossary

- BTP: Business Technology Platform.
- ADT: ABAP Development Tools.

### Contact Information

For assistance during the session, reach out to:
Swarnava Chatterjee (<swarnava.chatterjee@sap.com>) (Product Manager, SAP Build)
