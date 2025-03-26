Here is a brief Product Requirements Document (PRD) for the Team Matchmaker and Project Associate (SIA), followed by a plan to integrate APIs to achieve the described functionality.

**Brief Product Requirements Document (PRD): Team Matchmaker and Project Associate (SIA)**

**1. Introduction:**

The Team Matchmaker and Project Associate (SIA) is an AI-powered assistant designed to streamline collaboration and knowledge management for project participants within the Art of Living community. SIA aims to enhance project engagement, ensure members stay informed, and facilitate the formation of effective teams by matching individuals with relevant projects based on their interests and skills.

**2. Goals:**

*   Automate the initial setup of project knowledge bases using NotebookLM.
*   Facilitate easy access to project-related information for WhatsApp group members.
*   Enable seamless recording of project updates in Google Docs.
*   Provide quick answers to project-related queries using AI.
*   **Enable members to define their areas of interest for future projects.**
*   **Allow members to specify their current contribution areas within projects.**
*   **Classify existing projects based on predefined categories of interest and contribution areas.**
*   **Recommend relevant projects to members based on their stated interests and current contributions.**

**3. Target Users:**

*   Art of Living community members participating in seva or other projects.
*   Project leaders and organizers seeking to improve team coordination and information dissemination.
*   Individuals looking for seva opportunities aligned with their interests and skills.

**4. Key Features:**

*   **Automatic NotebookLM Space Creation:** Upon adding SIA to a WhatsApp group, a new NotebookLM workspace is automatically created, named after the group [History].
*   **Automatic Member Registration:** Members of the WhatsApp group are considered registered for the project within the NotebookLM space [History].
*   **Google Drive Integration:** SIA automatically identifies and integrates Google Drive links shared in the WhatsApp group description as source documents in the newly created NotebookLM space [History].
*   **Google Doc Update via WhatsApp:** Members can send messages addressed to "SIA" in the WhatsApp group to append the content of the message to a designated Google Doc associated with the project [History].
*   **AI-Powered Question Answering:** Members can ask SIA questions related to the project by mentioning her in the WhatsApp group or via direct message (DM). SIA will query the connected NotebookLM workspace and provide answers based on the source documents [History].
*   **User Profile Management:** Members can define their areas of interest for future projects and their current contribution areas for ongoing projects. This data will be stored [Implicit based on new feature].
*   **Project Classification:** Projects are categorized based on predefined areas of interest and required contribution types [Implicit based on new feature].
*   **Project Recommendation:** SIA recommends relevant projects to members based on the alignment between their defined interests, current contributions, and project classifications [Implicit based on new feature].

**API Integration Plan:**

This plan outlines the steps to integrate the necessary APIs to achieve the functionality of SIA. We assume a local version of NotebookLM is available with appropriate APIs [Query].

**Phase 1: Core Functionality (WhatsApp, NotebookLM, Google Drive Integration)**

1.  **WhatsApp API Integration:**
    *   **Objective:** Enable SIA to join WhatsApp groups, read group metadata (name, description, member list, messages), and send messages.
    *   **Steps:**
        *   Utilize the **WhatsApp Business API** or a similar interface (depending on availability for the assumed "SIA associate" bot account) to register and connect SIA.
        *   Implement a mechanism to **detect when SIA is added to a new WhatsApp group.** This might involve polling group membership changes or using webhook notifications if the API supports it.
        *   Upon being added, **retrieve the group name** using the API to name the NotebookLM space [History].
        *   **Read the WhatsApp group description** using the API to extract Google Drive links [History].
        *   Implement functionality to **send messages to the group** to confirm workspace creation and provide instructions [History].
        *   Continuously **monitor new messages** in the group using the API [History].

2.  **Local NotebookLM API Integration:**
    *   **Objective:** Create and manage NotebookLM workspaces and add Google Drive content as sources.
    *   **Steps:**
        *   Utilize the **local NotebookLM API** to **create a new workspace** with the name obtained from the WhatsApp group [History].
        *   Implement functionality to **take the extracted Google Drive links** and use the NotebookLM API to **add them as data sources** to the newly created workspace [History]. This might involve the API fetching content from the URLs or requiring authentication and direct file uploads depending on the NotebookLM API capabilities.
        *   Implement the **querying functionality:** When a message directed to SIA is detected in WhatsApp (e.g., "@SIA [question]"), the text of the question will be extracted and sent to the NotebookLM API. The API's response will then be formatted and sent back to the WhatsApp group via the WhatsApp API [History].

3.  **Google Drive API Integration:**
    *   **Objective:** Authenticate and append content to a designated Google Doc.
    *   **Steps:**
        *   Establish **OAuth 2.0 authentication** to allow SIA to access and modify Google Docs on behalf of an authorized account.
        *   Implement a mechanism for a project (e.g., the WhatsApp group creator or an admin) to **designate a specific Google Doc** for updates. This could be done via a specific command to SIA in the WhatsApp group (e.g., "@SIA set document [Google Doc Link]").
        *   When SIA detects a message addressed to it (e.g., "SIA, [update content]"), extract the "[update content]" and use the **Google Docs API** to **append this content to the designated Google Doc** [History].

**Phase 2: User Profiles, Project Classification, and Recommendations**

1.  **Develop User Profile Storage:**
    *   Design a database schema to store user information, including their WhatsApp ID (for linking), areas of interest for future projects (e.g., teaching, event organizing, content creation), and current contribution areas within active projects (e.g., social media, fundraising, technical support) [Implicit based on new feature].
    *   Create API endpoints or database access methods to allow users to update their profile information. This could be via a web interface or commands within WhatsApp directed to SIA.

2.  **Implement Project Classification:**
    *   Define a set of categories for classifying projects based on required areas of interest and contribution types [Implicit based on new feature].
    *   Develop a mechanism for project creators or administrators to classify their projects according to these categories. This could also be managed through a web interface or WhatsApp commands. Store this project metadata in a database linked to the NotebookLM workspace or the WhatsApp group ID.

3.  **Develop Recommendation Logic:**
    *   Create an algorithm that compares a user's defined areas of interest and current contributions with the classifications of existing projects [Implicit based on new feature].
    *   Implement functionality for SIA to trigger project recommendations to users. This could be based on:
        *   New user joining the platform.
        *   User updating their profile.
        *   Periodically scanning for new projects that match user profiles.
    *   Recommendations could be sent via WhatsApp DM from SIA to the user.

4.  **Integrate User Data with NotebookLM (Optional but Recommended):**
    *   Explore the possibility of enriching the NotebookLM workspace with user-specific information (interests, contributions) to provide more context-aware answers to queries or to tailor recommended resources within the workspace in the future. This would require further investigation into the capabilities of the local NotebookLM API.

By following this phased approach, the Team Matchmaker and Project Associate (SIA) can be developed to effectively support collaboration, knowledge sharing, and team formation within the Art of Living community, leveraging the power of AI and seamless API integrations.
