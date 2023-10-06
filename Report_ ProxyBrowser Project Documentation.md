# Table of Contents

- [Table of Contents](#table-of-contents)
- [Report: ProxyBrowser Project Documentation](#report-proxybrowser-project-documentation)
  - [Introduction](#introduction)
  - [Getting Started](#getting-started)
  - [Project Overview](#project-overview)
  - [Development Guidelines](#development-guidelines)
  - [Additional Resources](#additional-resources)



# Report: ProxyBrowser Project Documentation

## Introduction

1. ### Project Overview
    ProxyBrowser represents a sophisticated web browsing application meticulously crafted with an emphasis on user security and customization. It encompasses an extensive array of features meticulously designed to elevate the online experience, catering specifically to users who prioritize privacy and seek greater control over their browsing activities.

2. ### Purpose of Documentation
    The purpose of this documentation is to provide a clear understanding of the ProxyBrowser project, its functionality, development processes, and how to contribute to its growth. It serves as a reference for developers, contributors, and users.

3. ### Audience
    This documentation is intended for: 
- Developers and contributors interested in understanding and contributing to the ProxyBrowser project.
- Users seeking information on ProxyBrowser\'s features and functionality.
- Project managers and stakeholders looking for an overview of the project\'s structure and development guidelines.

## Getting Started
Currently, we have three repositories: one dedicated to Front-end development, another for Back-end, and a third one specifically for the browser.
- Front-End: \"**proxy-browser**\".
- Back-End: \"**proxy-browser-backend**\".
- Browser: \"**wexond-browser-extended**\"

1. ### Wexond-Browser-Extended 
    1.1. **Setting Up the Development Environment**
    Before beginning, it\'s crucial to ensure that your current Node.js and npm versions are compatible with the project\'s requirements. Please follow these steps to prepare your environment:
    -  **To verify your node and yarn version**
        - `node --version`
        - `yarn --version`
    - **How To Install specific node version**
        - ```nvm install 14.9.0``` (nvm is the node version manager)
        - ```nvm use 14.9.0```
    - Set env variables through terminal
    - **To initialise the project in development mode for the first time, please follow these steps:** 
        - ```yarn rebuild```
        - ```yarn dev```
    - **For subsequent runs in development mode, use the following command:**
        - ```yarn dev```

2. ### Proxy-Browser-Backend
    2.1. **Setting Up the Development Environment**
    - Create a file named ".env" at the root level of the folder.
    - Define env variables into it.
    - **To initialise the project in development mode for the first time, please follow these steps:**
        - ```npm run db:migrate```
        - ```npm run stripe:seeder```
        - ```npm run dev```
    - **For subsequent runs in development mode, use the following command:**
        - ```npm run dev```
    - **If you need to make changes to the database through migrations, perform the following steps:**
        - ```npm run generate-migration -- --name <migration-name>```
        - ```npm run db:migrate```
    - **To revert changes made by a migration, use the command:**
        - ```npm run db:migrate:undo```

    2.2. **Project Structure**
    The project adheres to a standard directory structure typical of a **Node.js/Express** backend project. It is organised as follows:
    - **config** - Configuration files that store settings and parameters for the database
    - **controllers** - Modules responsible for handling incoming HTTP requests, processing data, and sending appropriate responses.
    - **joiSchemas** - Schemas defined using the Joi library to validate and sanitise incoming data from requests.
    - **middlewares** - Functions that intercept and process requests before they reach the controller.
    - **models** - Representations of database tables.
    - **routes** - Definitions for the URL endpoints of API, mapping incoming requests to the appropriate controller methods.
    - **utils** - Utility functions and helper modules used throughout application for common tasks.
    - **views** - templates for rendering dynamic HTML content in email.
    - **app.js** - The entry point of Express application where you set up server configurations, middleware, and initialise routes.

3. ### Proxy-Browser
    3.1. **Setting Up the Development Environment**
    - **To run the project in development mode, execute the following command:**
        - ```REACT_SERVER_URL=http://<device_ip_address>:3000 yarn dev```

    3.2. **Project Structrue**
    The project follows a directory structure similar to that of a basic **React App**. It is organised as follows:
    - **public**
    - **electron.js** - Responsible for launching the project using Electron JS.
    - **Index.html** - Serves as the primary entry point for the application.
    - **src**
        - **assets** - This directory houses various project assets, including images, SVGs, and more.
        - **component** - Within this directory, you\'ll find the React components utilised in constructing pages.
        - **pages** - This directory is dedicated to housing the pages, which serve as containers for the React components.

## Project Overview
1. ### Project Goals
    The goal of the ProxyBrowser - Wexond Browser Extended project is to develop a feature-rich, user-friendly web browser application with enhanced privacy, security, and customization options. The project aims to provide users with a versatile and personalised browsing experience, while also prioritising their online privacy and data security.
2. ### Key Features
    Explore the core features of ProxyBrowser, including user authentication, proxy management, dedicated proxies, and more.
- **Separate Browser Instance**: Users can enjoy a dedicated and separate browser environment to maintain privacy and avoid interference with their main browsing session.
- **Downloading Files**: Users can initiate and manage downloads with a user-friendly interface, including specifying download locations and monitoring progress.

![Browser Download Settings Screen](/images/image-1.png)

- **Creating New Windows**: The browser supports multiple browser windows for multitasking and easy management of websites and tasks.

![Browser Screen with multiple windows](/images/image-2.png)

- **Managing Cookies**: Users have control over cookie settings, including enabling/disabling cookies, clearing cookies for specific sites, and managing preferences.
- **Local Storage**: HTML5 local storage support allows websites to store data on the user\'s device.
- **Search Engine Settings**: Users can select their preferred search engine from a list of options, with Google as the default engine.
  
![Browser Search Engine Setting Screen](/images/image-3.png)

- **Keyboard Shortcuts**: Enhanced keyboard shortcuts improve navigation efficiency, including tab management.
- **Proxy Support**: The browser offers support for a Las Vegas proxy, enabling IP address and location changes for enhanced privacy and access to geo-restricted content.
- **User Data and Sessions Isolation**: Each user\'s interactions are isolated, ensuring privacy and security. Separate directories and settings are created for each user.
- **Login/Sign up Functionality:**
    -  **Sign In**: Users can seamlessly access their accounts through a user-friendly interface by entering their credentials.
    -  **Sign Up**: New users can register securely, enabling enhanced features and personalised settings.

![Sign In Screen](/images/image-4.png)
![Sign Up Screen](/images/image-5.png)

- **Forgot Password Functionality:**
    -  **User Requests Password Reset**: Users can initiate a password reset by providing their email.
    -  **Send OTP (One-Time Password)**: A unique OTP is sent to the user\'s email for verification.
    -  **Enter OTP and Set New Password**: Users enter the OTP, set a new password, and regain access securely.

![Forgot Password Screen](/images/image-6.png)
![OTP Code Screen](/images/image-7.png)
![Set New Password Screen](/images/image-8.png)

- **Dashboard for Unique Proxies:**
    -  **Proxies Overview**: Users can monitor real-time proxy usage, performance, and status.
    -  **Filtering Capabilities**: Customizable data views with powerful filtering options based on location, speed, reliability, and more.
    -  **Proxy Management**: Easily add, edit, or remove unique proxies directly from the dashboard.

![Dashboard Screen](/images/image-9.png)

- **Creating A New Location:**
    -  **Name Your Location**: Users can name their new location for easy identification.
    -  **Set the Home Page URL**: Specify the home page URL for the new location.
    -  **Select the Country**: Choose the associated country from a dropdown menu.

![Create Location Screen](/images/image-10.png)

- **Edit/Delete A Location:** Users can access and manage created locations within the dashboard, edit/update location details, including name, URL, or country selection.

![Edit Location Screen](/images/image-11.png)

- **Dedicated Proxy:** Exclusive access to dedicated proxies ensures privacy, data security, and unrestricted browsing. Users can customise and configure dedicated proxies to meet their specific needs.

![Dashboard Screen](/images/image-12.png)

- **History Keeping:** Users can access, search, filter, sort, and organise their browsing history for a personalised experience.

![Browser History Screen](/images/image-13.png)

- **Tracking Protection:** The browser proactively identifies and blocks intrusive tracking technologies to safeguard online privacy. Users can tailor their privacy settings to match their preferences.

![Browser Privacy Settings Screen](/images/image-14.png)

- **Marking Page as Bookmark:** Users can mark web pages as bookmarks, making it easy to access and organise favourite and frequently visited websites.

![Browser Window with Bookmark Pop-up](/images/image-15.png)
![Browser Bookmarks Screen](/images/image-16.png)

- **Incognito Window:** Incognito Windows prioritise user privacy by not recording browsing history, storing cookies, cached data, or autofill data.

![Browser Incognito Screen](/images/image-17.png)

- **Browser Theme Settings:** Users can select themes (light, dark, custom) and customise the top bar variant and bookmarks settings.

![Browser Incognito Screen](/images/image-18.png)

- **Search Engine**: In wexond-browser there is an option for the user to select his search engine on a list of search engines provided. Previously the default engine was duckduckgo and now we have changed it to google, So now the default engine is google in our extended version. 
We achieve this by changing the settings data. First when a project runs it will store the settings data, cookies and local storage to a specific directory related to each user, After that It will read from that directory only, So to achieve this we have to remove settings and then make the build of the project again.
- **Keyboard Shortcuts**: In the extended version of Wexond Browser, additional keyboard shortcuts are introduced to enhance the user\'s browsing experience. Shortcuts can include actions like navigating between tabs, opening new tabs, closing tabs, and more. These shortcuts improve efficiency and navigation for power users. Users can manage multiple open tabs efficiently. They can switch between tabs using keyboard shortcuts or mouse interactions, reorder tabs, and close tabs as needed. Tab management is a crucial feature for users who regularly work with multiple websites simultaneously.
To achieve this we created an event that will shift tabs of the open windows and on the base of a specific key press, so whenever a user presses those keys he/she will be able to switch tabs. We use menu items to achieve the above discussed functionality, Menu items are used to
handle specific event on click.
- **Proxy Support**: Wexond Browser offers a unique feature by including support for a Las Vegas proxy. This proxy allows users to change their IP address and location, enhancing online privacy and enabling access to geo-restricted content. Users can configure proxy settings within the browser to route their web traffic through the Las Vegas proxy server.
Used proxy-chain package to implement proxy server and use os package to verify the contents of request and add proxy if request is of Ipv4. Set up a proxy server that listens on port 8080, forwards incoming requests to an upstream proxy server with authentication, and handles responses from the target server, including error handling. It also enables verbose logging for debugging and returns the proxy server instance for further use in the application.
- **Implemented separate user data and sessions for each instance:** In a browser app, separating user data and sessions for each instance means that each user\'s interactions with the application are isolated from one another. Each instance or user session operates independently, with its own set of data and settings, ensuring privacy and security. This separation prevents one user\'s actions from affecting or accessing the data or session of another user, creating a distinct and personalized experience for each person using the application. This approach is essential for maintaining user privacy, data integrity, and security in multi-user web applications.
To achieve this functionality, we create a unique time stamped directory for each user. If the directory already exists, it writes the data into the existing directory, if the directory does not exist, it creates a new one. By using this approach, we can set cookies, local storage, and sessions for each user separately.
- **Models:** In the proxy-browser-backend, our project incorporates models for User, Location, OTP, PaymentMethod, Plan, and Session, which directly correspond to the database tables. These models serve as integral components employed consistently throughout the project for querying purposes. The implementation of these models is facilitated by Sequelize, a choice made for its ease of query construction and its inherent safeguard against SQL injection attacks. Additionally, we have opted to employ a MySQL database in conjunction with Sequelize.
- **Stripe:** Our services are offered on a paid basis, and upon user registration, individuals are granted a complimentary 7-day trial period. Following this trial period, users will be billed in accordance with their chosen subscription plan. It is our commitment to ensure that users remain within our application throughout this process, offering a seamless experience. To realize this functionality, we have seamlessly integrated Stripe into our system. Upon user registration, we not only establish them as Stripe customers but also enroll them in our plan, which includes a 7-day trial period. During this time frame, users have the option to securely add their preferred payment method. Subsequently, once the trial period concludes, automatic billing for our services commences. 
- **REST API:** In order to ensure a smooth and seamless user experience within our application, we have meticulously developed a REST API that encompasses comprehensive functionalities for all models. For users, it includes features such as registration, login, profile updating, and password reset. Location-related functions comprise location creation, updating, retrieval of user-specific locations, accessing individual locations, and deletion. OTP functionalities encompass OTP generation and validation. Users can also add payment methods, create or revoke plans, and manage sessions through complete CRUD operations. Furthermore, our API is fortified with request validations using Joi schemas and seamlessly integrates with Stripe for payment processing.


## Development Guidelines
1. **Coding Standards**

    ProxyBrowser has been meticulously developed, adhering to industry-leading coding practices, in order to uphold superior code quality  and long-term maintainability.
2. **Competitor**
   
    We utilise Git and GitHub for version control purposes.
3. **Code Review Process**
   
    For code review, we maintain an internal Slack channel dedicated to the process, where we request our team to review our code.
  
## Additional Resources
1. **Relevant Links**

    Please locate the links to the repositories:
   - [wexond-browser-extended](https://github.com/qbatch/wexond-browser-extended)
   - [proxy-browser-backend](https://github.com/qbatch/proxy-browser-backend)
   - [proxy-browser](https://github.com/qbatch/proxy-browser)
2. **Competitor**
   
    One of our primary competitors in the market is [Mirage](https://mirageid.com/)
