---
title: Knowledge Base Best Practices
excerpt: >-
  Set up Knowledge Bases effectively by prioritizing structured data, ensuring
  data quality, and using automated ingestion tools.
deprecated: false
hidden: true
metadata:
  robots: index
---
The efficiency of your Botpress chatbot relies heavily on the quality of the data fed into the Knowledge Base (KB). This document outlines best practices for setting up your KB to ensure optimal performance and accurate chatbot responses.

1. Structured vs. Unstructured Information\
   The success of your chatbot depends on how well the information in your KB is structured:
   Structured Data: Always prioritize structured data. It leads to more accurate and relevant answers. If your information can be categorized or broken down into fields or columns, use Tables in the Botpress KB.
   Unstructured Data: When structured data isn’t available, use Rich Text for plain text information. This allows the AI to effectively parse through the content. Rich Text often works best for logically organized, though unstructured, content.

2. Garbage In, Garbage Out\
   The quality of the data you feed into the KB directly impacts the quality of the chatbot's responses. Ensure the information is:
   Accurate
   Current
   Free from unnecessary or redundant details
   Poor-quality data will lead to poor chatbot performance. When planning an AI Agent project that requires KB ingestion, consider doing a redundant, obsolete, or trivial (ROT) analysis of the KB source.

3. Choosing the Right Knowledge Type\
   When populating your KB, it’s essential to use the correct type based on the nature of your information:
   Tables: Best suited for structured data. If your information can be classified by attributes or specific fields, using Tables will make it easier for the bot to search and extract data. Examples of structured data include FAQ question/answer sets, product information, support ticket data, legal agreements, etc.
   Rich Text: Use this for unstructured but logically organized content. It’s a great solution when tables aren’t feasible.
   Documents (PDF, HTML, .doc, .txt): Only use documents when the data can’t be easily represented as structured or plain text. Keep in mind that when documents are uploaded, all styles and images are removed, so structure them accordingly.

4. Using Website Crawlers and Search Engines\
   Botpress offers flexible options for ingesting website data into the KB:
   Valid Sitemap: If your website has a valid sitemap, use the Website crawler, which ingests information more effectively. Tools such as:
   Sitemap Finder
   Sitemap Validator
   can help verify the sitemap’s validity.
   No Valid Sitemap: If your website lacks a valid sitemap, use the Search The Web feature, which relies on Bing search to extract relevant information from the web.
   Manual Crawling: For more manual, specific crawling tasks, you can integrate additional solutions or manually validate crawled content.

5. Autonomous Node for Optimized Results\
   For KBs built with Tables, using the Autonomous Node feature is recommended. It helps the bot find more accurate answers by pinpointing relevant information within the table.
   Note: there are important configuration that you need to understand how Autonomous node works. \[Learn more about autonomous nodes here].

6. FAQs First, Knowledge Base Second\
   To optimize response efficiency, always query your FAQs tables first before moving on to the broader knowledge base. FAQs are often concise and provide direct answers to common questions.
   Note: there are important configuration that you need to understand in order to get your ai spend down. \[Read more about AI optimization in our blog].

7. Document Ingestion\
   When ingesting files (PDFs, Word documents, etc.), Botpress removes styles, images, and tables during the ingestion process. Ensure that your documents are structured properly so that critical information is retained and parsed by the bot effectively.

8. Other Methods for Ingesting Knowledge into the KB\
   In addition to manually uploading files, Botpress provides automated methods for ingesting data into the KB, ensuring that your chatbot remains up to date with the latest information.
   Direct API Calls (Files API): You can integrate Botpress with your existing systems and applications to insert documents or other data directly into the KB.
   Example: Your CRM system sends updated product info to Botpress KB automatically when a new product is added.
   Fixed Scheduler (Cron Job): Set up a Cron Job that periodically calls your APIs to fetch data, which can then be synced to a KB or table in Botpress using an Execute Code Card.
   Example: A nightly task pulls inventory data from your ERP system, updating a table in the KB with new product details.
   Webhook (Trigger): External systems (such as Jira, Zendesk, or other third-party apps) can push data directly to Botpress through webhooks. In Botpress, this data can be processed and synced to a KB or table via an Execute Code Card.
   Example: When a new support ticket is created in Zendesk, a webhook sends relevant details to Botpress to keep the bot updated with the latest customer issues.
   Adding extra preprocessing steps in the Execute Code Card can ensure the incoming data is well-prepared for the KB.
   By using these automated ingestion methods, your Knowledge Base stays current without requiring constant manual updates.

9. Conversation Design\
   When designing conversations, it's important to segregate information based on the input and flow of data. Group related content together, and consider breaking down large knowledge areas into smaller, manageable sections for more accurate responses. Avoid overwhelming the chatbot with a single large KB.
   For example, if you have two separate products detailed in one document, it’s better to split them into separate PDFs, ideally within two separate KBs, for clearer responses and easier management.

Conclusion\
Following these best practices will ensure your chatbot provides accurate, relevant, and timely information. Prioritize structured data, choose the appropriate KB type, and leverage automated ingestion tools to keep your bot’s knowledge up-to-date and functioning optimally.