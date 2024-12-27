---
title: Welcome
deprecated: false
hidden: false
metadata:
  title: Botpress Documentation
  description: >-
    Botpress is an all-in-one platform for build AI agents powered by the latest
    LLMs.
  keywords:
    - botpress
    - documentation
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
        :root {
            --primary-color: #2563eb;
            --secondary-color: #3b82f6;
            --text-color: #1f2937;
            --bg-color: #f8fafc;
            --card-bg: #ffffff;
            --hover-color: #1d4ed8;
        }

        body {
            font-family: 'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
            margin: 0;
            padding: 0;
            background-color: var(--bg-color);
            color: var(--text-color);
            line-height: 1.6;
            background-image: 
                radial-gradient(circle at 100% 100%, rgba(37, 99, 235, 0.05) 0%, transparent 50%),
                radial-gradient(circle at 0% 0%, rgba(59, 130, 246, 0.05) 0%, transparent 50%);
            background-attachment: fixed;
        }

        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px 20px;
        }

        .header {
            text-align: center;
            margin-bottom: 60px;
            display: flex;
            align-items: flex-end;
            justify-content: center;
            gap: 16px;
        }

        .header svg {
            width: 48px;
            height: 48px;
            margin-bottom: 19px;
        }

        .header h1 {
            font-size: 3.5em;
            margin: 0;
            background: linear-gradient(135deg, var(--primary-color), var(--secondary-color));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            margin-bottom: 20px;
            line-height: 1;
        }

        .grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 30px;
            margin-top: 40px;
            animation: fadeIn 0.6s ease-out;
        }

        .card {
            background: var(--card-bg);
            padding: 32px;
            border-radius: 16px;
            box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.1), 0 2px 4px -2px rgb(0 0 0 / 0.1);
            transition: transform 0.2s ease, box-shadow 0.2s ease;
            position: relative;
            overflow: hidden;
        }

        .card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            right: 0;
            height: 4px;
            background: linear-gradient(90deg, var(--primary-color), var(--secondary-color));
            transform: translateY(-100%);
            transition: transform 0.3s ease;
        }

        .card:hover::before {
            transform: translateY(0);
        }

        .card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 15px -3px rgb(0 0 0 / 0.1), 0 4px 6px -4px rgb(0 0 0 / 0.1);
        }

        .card h2 {
            font-size: 1.8em;
            margin-bottom: 20px;
            color: var(--primary-color);
            display: flex;
            align-items: center;
        }

        .card p {
            color: #4b5563;
            margin-bottom: 25px;
        }

        .btn {
            display: inline-block;
            padding: 12px 24px;
            font-size: 1em;
            font-weight: 600;
            color: #fff;
            background-color: var(--primary-color);
            text-decoration: none;
            border-radius: 8px;
            transition: all 0.2s ease;
            position: relative;
            overflow: hidden;
        }

        .btn::after {
            content: '';
            position: absolute;
            width: 100%;
            height: 100%;
            top: 0;
            left: 0;
            background: rgba(255, 255, 255, 0.1);
            transform: translateX(-100%);
            transition: transform 0.3s ease;
        }

        .btn:hover::after {
            transform: translateX(0);
        }

        .btn:hover {
            background-color: var(--hover-color);
            transform: translateY(-2px);
        }

        .links-container {
            margin-top: 30px;
        }

        .sub-link {
            display: block;
            padding: 12px 16px;
            margin: 10px 0;
            color: var(--text-color);
            text-decoration: none;
            border-radius: 8px;
            transition: all 0.2s ease;
            background-color: #f1f5f9;
        }

        .sub-link:hover {
            background-color: #e2e8f0;
            color: var(--primary-color);
            padding-left: 20px;
        }

        @media (max-width: 768px) {
            .container {
                padding: 20px;
            }
            
            .header h1 {
                font-size: 3em;
            }
            
            .card {
                padding: 24px;
            }
        }

        .header-description {
            text-align: center;
            margin-bottom: 40px;
        }

        .header-description p {
            font-size: 1.2em;
            color: #4b5563;
            max-width: 600px;
            margin: 0 auto;
        }

        @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <svg width="32" height="32" viewBox="0 0 32 32" fill="none" xmlns="http://www.w3.org/2000/svg">
                <rect width="32" height="32" rx="8" fill="#21201C"/>
                <path fill-rule="evenodd" clip-rule="evenodd" d="M21.0204 17.5548L23.5267 18.978C23.8173 19.1381 24.017 19.4583 23.9989 19.7963V22.6249C23.9989 22.963 23.8173 23.2654 23.5267 23.4433L21.0204 24.8666C20.7298 25.0445 20.3666 25.0445 20.0578 24.8666L17.5516 23.4433C17.2611 23.2833 17.0612 22.963 17.0795 22.6249V19.9565L11.2315 16.6475L12.3757 18.3198L10.941 19.1381C10.6504 19.316 10.2872 19.316 9.97842 19.1381L7.47219 17.7148C7.18161 17.5548 7 17.2523 7 16.9144V14.0679C7 13.7299 7.18161 13.4274 7.47219 13.2495L9.97842 11.8264C10.269 11.6484 10.6322 11.6484 10.941 11.8264L12.1941 12.5379L13.3019 13.1605L17.0795 11.0258V8.375C17.0795 8.03698 17.2611 7.73455 17.5516 7.55665L20.0578 6.13342C20.3484 5.95553 20.7116 5.95553 21.0204 6.13342L23.5267 7.55665C23.8173 7.71676 24.017 8.03698 23.9989 8.375V11.2037C23.9989 11.5417 23.8173 11.8441 23.5267 12.022L21.0204 13.4452C20.7298 13.6231 20.3666 13.6231 20.0578 13.4452L18.8047 12.7336L18.7321 12.698L20.0578 10.7945L17.715 12.1288L13.9376 14.2635V16.772L17.715 18.9068L18.8229 18.2842L20.076 17.5726C20.3484 17.3769 20.7298 17.3947 21.0204 17.5548Z" fill="#FDFDFC"/>
            </svg>
            <h1>Botpress Documentation</h1>
        </div>
        <div class="header-description">
            <p>Botpress is an all-in-one platform for building AI agents powered by the latest LLMs.</p>
        </div>
        <div class="grid">
            <div class="card">
                <h2>
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" style="margin-right: 8px;">
                        <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2V3zm20 0h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7V3z" stroke="currentColor" stroke-width="2"/>
                    </svg>
                    Guides
                </h2>
                <p>Explore Botpress features, tools, and best practices for building and deploying AI chatbots and agents.</p>
                <a href="/docs/build" class="btn">Browse Guides</a>
                
                <div class="links-container">
                    <h3>Popular Pages</h3>
                    <a href="/docs/embedded-webchat-getting-started" class="sub-link">Place a bot on your website</a>
                    <a href="/docs/variables" class="sub-link">Use variables to store data</a>
                    <a href="/docs/using-integrations" class="sub-link">Install an integration</a>
                </div>
            </div>
            
            <div class="card">
                <h2>
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="currentColor" style="margin-right: 8px;">
                        <path d="M20 4C21.1 4 22 4.9 22 6V18C22 19.1 21.1 20 20 20H4C2.9 20 2 19.1 2 18V6C2 4.9 2.9 4 4 4H20M20 18V8H4V18H20M9 10H7V16H9V10M13 10H11V16H13V10M17 10H15V16H17V10Z"/>
                    </svg>
                    API Reference
                </h2>
                <p>Dive into technical insights about Botpress API endpoints to integrate and extend the platform effectively.</p>
                <a href="/reference/introduction" class="btn">View API Docs</a>
                
                <div class="links-container">
                    <h3>Popular Pages</h3>
                    <a href="https://botpress.com/reference/createconversation" class="sub-link">Manage conversations</a>
                    <a href="https://botpress.com/reference/what-is-the-files-api" class="sub-link">Manage files</a>
                    <a href="https://botpress.com/reference/introduction" class="sub-link">Learn about the Chat API</a>
                </div>
            </div>
        </div>
    </div>
</body>
</html>
`}</HTMLBlock>