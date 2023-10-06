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
    ProxyBrowser represents a cutting-edge web browsing application meticulously developed to prioritize user security as its core principle. With an unwavering commitment to enhancing the online experience, ProxyBrowser offers a comprehensive suite of features that have been thoughtfully customized to cater to the discerning needs of individuals who value privacy and seek a high degree of control over their online activities. By seamlessly integrating state-of-the-art security measures and a rich feature set, ProxyBrowser ensures that users can navigate the web with confidence, safeguarding their digital presence while optimizing their browsing experience.

2. ### Purpose of Documentation
    The purpose of this documentation is to provide a clear understanding of the ProxyBrowser project, its functionality, development processes, and how to contribute to its growth. It serves as a reference for developers, contributors, and users.

3. ### Audience
    This documentation is intended for: 
- Developers and contributors interested in understanding and contributing to the ProxyBrowser project.
- Users seeking information on ProxyBrowser\'s features and functionality.
- Project managers and stakeholders looking for an overview of the project\'s structure and development guidelines.

## Getting Started
Currently, we have three repositories: one dedicated to Front-end development, another for Back-end, and a third one specifically for the browser.
- Front-End: \"**proxy-browser**\"
- Back-End: \"**proxy-browser-backend**\"
- Browser: \"**wexond-browser-extended**\"

1. ### Wexond-Browser-Extended 
    1.1. **Setting Up the Development Environment**
    Before beginning, it\'s crucial to ensure that your current Node.js and npm versions are compatible with the project\'s requirements. Please follow these steps to prepare your environment:
    -  **To verify your node and yarn version**
      
        -     node --version
    - **How To Install Specific Node Version**
        - **In Mac OS**
          - **using brew**
            
            -     brew install node@14.9.0
            -     brew unlink node
            -     brew link node@14.9.0
            -     node -v
          - **using nvm (Node Version Manager)**
            -   To install nvm in Mac OS follow this [link](https://tecadmin.net/install-nvm-macos-with-homebrew/)
              
            -     nvm install 14.9.0
            -     nvm use 14.9.0
        - **In Windows**
          - **using nvm (Node Version Manager)**
            -   To install nvm on a Windows system, you can use this [download link](https://github.com/coreybutler/nvm-windows/releases/download/1.1.11/nvm-setup.exe) for the nvm setup.
              
            -     nvm install 14.9.0
            -     nvm use 14.9.0
        - **In Linux/Ubuntu**
          - **using nvm (Node Version Manager)**
            -   To install nvm in Mac OS follow this [link](https://tecadmin.net/how-to-install-nvm-on-ubuntu-22-04/)
              
            -     nvm install 14.9.0
            -     nvm use 14.9.0
    - Set env variables through the terminal
    - **To initialize the project in development mode for the first time, please follow these steps:**
      
        -     yarn rebuild
        -     yarn dev
    - **For subsequent runs in development mode, use the following command:**
      
        -     yarn dev

2. ### Proxy-Browser-Backend
    2.1. **Setting Up the Development Environment**
    - Create a file named ".env" at the root level of the folder.
    - Define env variables into it.
    - **To initialize the project in development mode for the first time, please follow these steps:**
      
        -     npm run db:migrate
        -     npm run stripe:seeder
        -     npm run dev
    - **For subsequent runs in development mode, use the following command:**
      
        -     npm run dev
    - **If you need to make changes to the database through migrations, perform the following steps:**
      
        -     npm run generate-migration -- --name <migration-name>
        -     npm run db:migrate
    - **To revert changes made by a migration, use the command:**
      
        -     npm run db:migrate:undo

    2.2. **Project Structure**
    The project adheres to a standard directory structure typical of a **Node.js/Express** backend project. It is organized as follows:
    - **config** - Configuration files that store settings and parameters for the database
    - **controllers** - Modules responsible for handling incoming HTTP requests, processing data, and sending appropriate responses.
    - **joiSchemas** - Schemas defined using the Joi library to validate and sanitize incoming data from requests.
    - **middlewares** - Functions that intercept and process requests before they reach the controller.
    - **models** - Representations of database tables.
    - **routes** - Definitions for the URL endpoints of API, mapping incoming requests to the appropriate controller methods.
    - **utils** - Utility functions and helper modules used throughout the application for common tasks.
    - **views** - templates for rendering dynamic HTML content in email.
    - **app.js** - The entry point of the Express application where you set up server configurations, middleware, and initialize routes.

    2.3. **Implementation Approach**
    - **Models:** In the proxy-browser-backend, our project incorporates models for User, Location, OTP, PaymentMethod, Plan, and Session,   which directly correspond to the database tables. These models serve as integral components employed consistently throughout the project for querying purposes. The implementation of these models is facilitated by Sequelize, a choice made for its ease of query construction and its inherent safeguard against SQL injection attacks. Additionally, we have opted to employ a MySQL database in conjunction with Sequelize.
    - **Attribute Knowledge**
      - **Users**
      
        | Attribute Name | Possible Values | Description |
        | ------------ | ------------ | ------------ |
        | email | Any Valid Email  | An email associated with user |
        | account_type | 'Personal', 'Business' | Type or level of user account |
        | password | Any Combination of Character  | Secure access code for the account |
        | first_name | String | First name of the user  |
        | last_name | String | Last name of the user |
        | country | Any valid country name | User's country of residence |
        | city | Any valid city name of entered country | User's city of residence |
        | state | Any valid state name of entered country | User's state of residence |
        | zip_code | 5-digit numeric code | User's postal code |
        | address | String | User's street address |
        | stripe_customer_id | String | Stripe Customer ID to manage subscription |

        - **Associations**
          -  A **User** have many **OTP**
          -  A **User** have many **PaymentMethods**
          -  A **User** have many **Plans**
          -  A **User** have many **Locations**
          -  A **User** have many **Sessions**

       - **Locations**

         | Attribute Name | Possible Values | Description |
         | ------------ | ------------ | ------------ |
         | name | String  | A name set by user for location |
         | home_page | Any Website's URL  | A home_page that will be opened when that location is used |
         | location | Valid Proxy Location  | A proxy Location |

          - **Associations**
            -  A **Location** belongs to a **User**
            -  A **Location** have one **Session**
              
       - **OTP**
         | Attribute Name | Possible Values | Description |
         | ------------ | ------------ | ------------ |
         | code | Any 4-character alphanumeric String  | A code to be entered by the user to reset password |
         | creation_timestamp | Timestamp | A timestamp when code was created |
         | expiry_timestamp | Timestamp  | A timestamp when the code will be expired |
         | is_used | true, false  | To check whether code is used or not |

         - **Associations**
            -  OTP **many-to-one** Users
          
       - **PaymentMethods**
         | Attribute Name | Possible Values | Description |
         | ------------ | ------------ | ------------ |
         | stripe_card_id | String | Stripe Customer ID to pay for subscription |
         | last_four | 4-characters long numeric string | to store the last 4-digits of the user's card |

         - **Associations**
            -  PaymentMethods **many-to-one** Users

       - **Plans**
         | Attribute Name | Possible Values | Description |
         | ------------ | ------------ | ------------ |
         | amount | Numeric String | The amount paid by the user for the plan |
         | buying_date | Date | Date at which amount was paid by the user  |
         | expiry_date | Date | Date at which plan will be expired |
         | subscription_id | String | Stripe Subscription ID of the user |
         | status | "active", "cancelled" | Whether plan is currently active or cancelled by the user |

          - **Associations**
            -  Plans **many-to-one** Users
           
       - **Sessions**
         | Attribute Name | Possible Values | Description |
         | ------------ | ------------ | ------------ |
         | created_timestamp | Timestamp | A timestamp when the session was created |
         | last_used_timestamp | Timestamp | A timestamp when the session was last used by the user |
         | is_active | true, false | TO check if the session is active or not |
         | device_info | String | To store the info related to the device from which the user is accessing the app |

         - **Associations**
            -  Sessions **many-to-one** Users
            -  Sessions **one-to-one** Locations
    - **Stripe:** Our services are offered on a paid basis, and upon user registration, individuals are granted a complimentary 7-day trial period. Following this trial period, users will be billed in accordance with their chosen subscription plan. It is our commitment to ensure that users remain within our application throughout this process, offering a seamless experience. To realize this functionality, we have seamlessly integrated Stripe into our system. Upon user registration, we not only establish them as Stripe customers but also enroll them in our plan, which includes a 7-day trial period. During this time frame, users have the option to securely add their preferred payment method. Subsequently, once the trial period concludes, automatic billing for our services commences. 
    - **REST API:** In order to ensure a smooth and seamless user experience within our application, we have meticulously developed a REST API that encompasses comprehensive functionalities for all models. For users, it includes features such as registration, login, profile updating, and password reset. Location-related functions comprise location creation, updating, retrieval of user-specific locations, accessing individual locations, and deletion. OTP functionalities encompass OTP generation and validation. Users can also add payment methods, create or revoke plans, and manage sessions through complete CRUD operations. Furthermore, our API is fortified with request validations using Joi schemas and seamlessly integrates with Stripe for payment processing.

4. ### Proxy-Browser
    3.1. **Setting Up the Development Environment**
    - **To run the project in development mode, execute the following command:**
   
        -     REACT_SERVER_URL=http://<device_ip_address>:3000 yarn dev

    3.2. **Project Structure**
    The project follows a directory structure similar to that of a basic **React App**. It is organized as follows:
    - **public**
    - **electron.js** - Responsible for launching the project using Electron JS.
    - **Index.html** - Serves as the primary entry point for the application.
    - **src**
        - **assets** - This directory houses various project assets, including images, SVGs, and more.
        - **component** - Within this directory, you\'ll find the React components utilised in constructing pages.
        - **pages** - This directory houses the pages, which serve as containers for the React components.

    3.3. **Implementation Approach**
     - **JSX:** To achieve a dynamic and versatile user interface, we harnessed the power of JSX (JavaScript XML) in conjunction with the React framework. This strategic choice empowered us to create highly dynamic user interfaces and to break down these interfaces into modular components, fostering code reusability. By leveraging JSX and React's capabilities, we were not only able to craft fluid and responsive displays but also to encapsulate functionality within reusable components, optimizing the efficiency and maintainability of our codebase. This approach not only promotes a more dynamic user experience but also streamlines the development process, ultimately enhancing code maintainability and extensibility for future iterations of our project.
     - **MUI:** In our development process, we expedited our workflow by integrating Material UI components into our project architecture. This allowed us to leverage a rich array of meticulously crafted, pre-optimized components. These components not only significantly accelerated our development pace but also provided the flexibility to tailor their appearance to align seamlessly with our project's theme requirements. By harnessing the power of Material UI, we ensured a cohesive and polished user interface while streamlining our development efforts. 

## Project Overview
1. ### Project Goals
    The goal of the ProxyBrowser project is to develop a feature-rich, user-friendly web browser application with enhanced privacy, security, and customization options. The project aims to provide users with a versatile and personalized browsing experience, while also prioritizing their online privacy and data security.
2. ### Key Features Along with User Interface
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
    -  **Sign Up**: New users can register securely, enabling enhanced features and personalized settings.

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

- **Dedicated Proxy:** Exclusive access to dedicated proxies ensures privacy, data security, and unrestricted browsing. Users can customize and configure dedicated proxies to meet their specific needs.

![Dashboard Screen](/images/image-12.png)

- **History Keeping:** Users can access, search, filter, sort, and organize their browsing history for a personalized experience.

![Browser History Screen](/images/image-13.png)

- **Tracking Protection:** The browser proactively identifies and blocks intrusive tracking technologies to safeguard online privacy. Users can tailor their privacy settings to match their preferences.

![Browser Privacy Settings Screen](/images/image-14.png)

- **Marking Page as Bookmark:** Users can mark web pages as bookmarks, making it easy to access and organize favorite and frequently visited websites.

![Browser Window with Bookmark Pop-up](/images/image-15.png)
![Browser Bookmarks Screen](/images/image-16.png)

- **Incognito Window:** Incognito Windows prioritizes user privacy by not recording browsing history, storing cookies, cached data, or autofilling data.

![Browser Incognito Screen](/images/image-18.png)

- **Browser Theme Settings:** Users can select themes (light, dark, custom) and customize the top bar variant and bookmarks settings.

![Browser Incognito Screen](/images/image-17.png)

- **Search Engine**: In wexond-browser there is an option for the user to select his search engine on a list of search engines provided. Previously the default engine was Duckduckgo and now we have changed it to Google, so the default engine is Google in our extended version. 
We achieve this by changing the settings data. First, when a project runs it will store the settings data, cookies, and local storage in a specific directory related to each user, After that It will read from that directory only, to achieve this we have to remove settings and then make the build of the project again.
- **Keyboard Shortcuts**: In the extended version of Wexond Browser, additional keyboard shortcuts are introduced to enhance the user\'s browsing experience. Shortcuts can include actions like navigating between tabs, opening new tabs, closing tabs, and more. These shortcuts improve efficiency and navigation for power users. Users can manage multiple open tabs efficiently. They can switch between tabs using keyboard shortcuts or mouse interactions, reorder tabs, and close tabs as needed. Tab management is a crucial feature for users who regularly work with multiple websites simultaneously.
To achieve this we created an event that will shift tabs of the open windows and on the base of a specific key press, so whenever a user presses those keys he/she will be able to switch tabs. We use menu items to achieve the above discussed functionality, Menu items are used to
handle specific events on click.
- **Proxy Support**: Wexond Browser offers a unique feature by including support for a Las Vegas proxy. This proxy allows users to change their IP address and location, enhancing online privacy and enabling access to geo-restricted content. Users can configure proxy settings within the browser to route their web traffic through the Las Vegas proxy server.
Used proxy-chain package to implement proxy server and used os package to verify the contents of the request and add proxy if the request is of Ipv4. Set up a proxy server that listens on port 8080, forwards incoming requests to an upstream proxy server with authentication, and handles responses from the target server, including error handling. It also enables verbose logging for debugging and returns the proxy server instance for further use in the application.
- **Implemented separate user data and sessions for each instance:** In a browser app, separating user data and sessions for each instance means that each user\'s interactions with the application are isolated from one another. Each instance or user session operates independently, with its own set of data and settings, ensuring privacy and security. This separation prevents one user\'s actions from affecting or accessing the data or session of another user, creating a distinct and personalized experience for each person using the application. This approach is essential for maintaining user privacy, data integrity, and security in multi-user web applications.
To achieve this functionality, we create a unique time-stamped directory for each user. If the directory already exists, it writes the data into the existing directory, if the directory does not exist, it creates a new one. Using this approach, we can set cookies, local storage, and sessions for each user separately.


## Development Guidelines
1. **Coding Standards**

    ProxyBrowser has been meticulously developed, adhering to industry-leading coding practices, in order to uphold superior code quality  and long-term maintainability.
2. **Competitor**
   
    We utilize Git and GitHub for version control purposes.
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
