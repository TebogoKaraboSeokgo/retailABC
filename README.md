retailABC
retailABC is a sample ASP.NET Core MVC web application that demonstrates how to use Azure Storage services for a retail system. It integrates: • Azure Table Storage → Customers, Products, Inventory data. • Azure Blob Storage → Multimedia (images, videos, audio). • Azure Queue Storage → Transaction & inventory messages (serialized as JSON). • Azure File Share → Arbitrary file uploads.

Features • Manage customers, products, and inventory in Azure Table Storage. • Store and display multimedia in Azure Blob Storage. • Record transactions (with customer + amount + description) in Queue Storage. • Record inventory updates (product, quantity change, reason, price) in Queue Storage. • Upload, edit, and delete files in Azure File Share. • Background service to process queued messages.

Prerequisites • .NET 8 SDK (or .NET 6/7 if your project uses LTS). • Visual Studio 2022 or VS Code. • An Azure Storage account. o Queues: transactions, inventory o Tables: Customers, Products, Inventory o Blob Container: media o File Share: files

Unzip File
Build and Run retailABC.sln
How to Use Transactions

Go to /Transactions.
Enter: a. Customer ID b. Amount c. Description
Click Create Transaction.
The transaction will appear in the list and is stored in Azure Queue Storage.
Inventory

Go to /Inventory.
Enter: a. Product ID b. Quantity Change c. Reason d. Price
Click Add Inventory Update.
The product update is displayed and pushed to the Inventory Queue.
Customers & Products • CRUD operations for Customers and Products use Azure Table Storage. • Access via /Customers and /Products.

File Share

Navigate to /FileShare.
Upload any file → it is saved to Azure File Share.
Files can be edited (rename) or deleted.
Media • Upload images/videos/audio to Azure Blob Storage. • Access via /Blob (depending on your controller routes).

Background Processing • The QueueProcessorHostedService runs continuously. • It dequeues Transactions and Inventory messages for processing. • Extend this service to push data into a database or reporting dashboard. Project Structure retailABC/ │── Controllers/ # MVC Controllers (Transactions, Inventory) │── Models/ # Data models (TransactionMessage, InventoryMessage, etc.) │── Services/ # Azure Storage services (Table, Blob, Queue, File) │── Views/ # Razor views │── Background/ # Hosted services (queue processor) │── wwwroot/ # Static assets │── appsettings.json # Configuration (add Azure Storage connection string)

Security Notes • Store secrets securely using Azure Key Vault or dotnet user-secrets (not in plain text). • Ensure HTTPS is enabled. • Validate and sanitize user input to avoid injection attacks.

