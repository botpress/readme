---
title: Home
deprecated: false
hidden: false
metadata:
  robots: index
---
<HTMLBlock>{`
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Botpress Documentation</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f9f9f9;
            color: #333;
        }
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 20px;
        }
        .header {
            text-align: center;
            margin-bottom: 40px;
        }
        .header h1 {
            font-size: 2.5em;
            margin: 0;
        }
        .columns {
            display: flex;
            flex-wrap: wrap;
            gap: 20px;
        }
        .column {
            flex: 1;
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
            text-align: center;
        }
        .column h2 {
            font-size: 1.8em;
            margin-bottom: 15px;
        }
        .column p {
            font-size: 1em;
            margin-bottom: 20px;
            line-height: 1.5;
        }
        .btn {
            display: inline-block;
            padding: 10px 20px;
            font-size: 1em;
            color: #fff;
            background-color: #007BFF;
            text-decoration: none;
            border-radius: 5px;
            transition: background-color 0.3s;
        }
        .btn:hover {
            background-color: #0056b3;
        }
        .sub-btn {
            display: block;
            margin: 10px auto;
            padding: 8px 15px;
            font-size: 0.9em;
            color: #fff;
            background-color: #6c757d;
            text-decoration: none;
            border-radius: 4px;
            transition: background-color 0.3s;
        }
        .sub-btn:hover {
            background-color: #5a6268;
        }
        @media (max-width: 768px) {
            .columns {
                flex-direction: column;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>Botpress Documentation</h1>
        
        </div>
        <div class="columns">
            <div class="column">
                <h2>Guides</h2>
                <p>Explore Botpress features, tools, and best practices for building and deploying AI chatbots and agents.</p>
              <a href="/guides" class="btn">Guides</a>
           <br>  <h2>Popular pages</h2>
                <a href="https://botpress.com/docs/webchat" class="sub-btn">Place a bot on your website</a>
           <br>     <a href="https://botpress.com/docs/variables" class="sub-btn">Use variables to store data</a>
           <br>     <a href="https://botpress.com/docs/integrations-1" class="sub-btn">Install an integration</a>
            </div>
            <div class="column">
                <h2>API Reference</h2>
                <p>Dive into technical insights about Botpress API endpoints to integrate and extend the platform effectively.</p>
                <a href="/api-reference" class="btn">API Reference</a>
          <br>    <h2>Popular pages</h2>
                <a href="https://botpress.com/reference/createconversation" class="sub-btn">Manage conversations</a>
           <br>   <a href="https://botpress.com/reference/what-is-the-files-api" class="sub-btn">Manage files</a>
           <br>     <a href="https://botpress.com/reference/introduction" class="sub-btn">Learn about the Chat API</a>
            </div>
        </div>
    </div>
</body>
</html>
`}</HTMLBlock>