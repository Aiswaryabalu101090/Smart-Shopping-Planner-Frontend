# Seamless API Development with Data API Builder

### Goals

Have you ever walked into a store, did some shopping, and headed back home only to find that you forgot to buy 60% of the items you needed to get?
I struggle with this very same issue and so I decided to create the ‘Smart Shopping Planner’, an application that will help me keep track of the items I need to buy and that I can easily update before and after shopping.

Smart Shopping Planner is a React application built using JavaScript, that stores data in an Azure SQL database. In this blog, I want to show you how incredibly easy it was to provide REST endpoints (you can work with GraphQL too) to connect the app to the database.

| **Goal**              | Learn how to seamlessly build APIs with Data API Builder                                   |
| ----------------------------- | --------------------------------------------------------------------- |
| **What will you learn**       | *JavaScript, React, Azure Static Web Apps, Azure Static Web Apps CLI, Data API Builder, Azure SQLAI*                                        |
| **What you'll need**          | *[Azure subscription](https://azure.microsoft.com), [Azure SQL Database Resource](https://portal.azure.com/#create/Microsoft.SQLDatabase), [GitHub](https://github.com/)* |
| **Duration**                  | *1h*                                                                |
| **Microsoft Cloud Topics taught**                  | *Azure Static Web Apps,* *Azure SQL Database*                                                                |
| **Just want to try the app or see the solution?** | *Link to Step by step guide*                          |
| **Slides** | Coming soon!

### Video
*https://youtu.be/gCrBSSOezSQ*

### Pre-Learning
Step-by-step Guide Blog

### Prerequisites
1. An Azure Subscription
1. Azure SQL Database

### Code Snippets
<details>
    <summary>Run the following SQL code to create a table that will store our shopping items.</summary>

        CREATE TABLE ShoppingItems (
            id INT IDENTITY(1,1) PRIMARY KEY,
             category VARCHAR(100),
                name VARCHAR(100),
                quantity INT,
                description VARCHAR(200),
                unitPrice DECIMAL(10, 2),
             totalPrice DECIMAL(10, 2)
            );
![Landing-page](/public/images/sql-db-create-table.png)
</details>

<details>
    <summary>Add an Item entity and specify the permission</summary>

    "Item": {
      "source": "dbo.ShoppingItems",
      "permissions": [
        {
          "actions": ["*"],
          "role": "anonymous"
        }
      ]
    }
</details>

<details>
    <summary>Write a function to create an item in our database and call it from the Add button.</summary>

    const createItemRequest = async () => {
        try {
            const response = await fetch('/data-api/rest/Item', {
                method: 'POST',
                headers: {
                    'Content-Type': 'application/json',
                    'X-MS-API-ROLE' : 'admin',
                },
                body: JSON.stringify({
                    category,
                    name,
                    quantity,
                    description
                })
            });
            const data = await response.json();
            if (response.ok){
                console.log(data);
            } else {
                throw new Error(data.error.message);
            }
        } catch (error) {
            console.error(error);
        }
    }
</details>
