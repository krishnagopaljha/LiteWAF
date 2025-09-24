MaxWAF 🛡️
==========

MaxWAF is an intelligent, proxy-based Web Application Firewall (WAF) designed to provide robust, context-aware protection for your web applications. It goes beyond simple pattern matching by using a threat-scoring engine to reduce false positives and implementing advanced normalization techniques to detect evasive attacks.

It inspects all incoming HTTP requests and leverages a Redis backend for high-performance rate limiting and IP banning. All detected threats are logged to a real-time security dashboard for immediate analysis.

Key Features
------------

*   **🧠 Intelligent Threat Scoring:** Instead of blocking on the first trigger, MaxWAF accumulates a threat score for each request. A request is only blocked if its score exceeds a configurable threshold, dramatically reducing false positives.
    
*   **🛡️ Comprehensive Threat Coverage:** Protects against a wide range of common and emerging vulnerabilities:
    
    *   SQL Injection (SQLi)
        
    *   Cross-Site Scripting (XSS)
        
    *   Command Injection
        
    *   XML External Entity (XXE)
        
    *   Directory Traversal
        
    *   Server-Side Request Forgery (SSRF)
        
    *   JWT alg:none Manipulation
        
*   **🤺 Adversarial Robustness:** Implements multi-layered input normalization (URL decoding, HTML entity decoding, lowercasing) to counter common evasion techniques used by attackers.
    
*   **⚡ High-Performance DDoS Protection:** Utilizes a Redis backend for fast, efficient rate limiting and temporary IP banning of malicious actors.
    
*   **📊 Real-time Security Dashboard:** A separate logger service provides a clean, web-based dashboard that displays all detected security events as they happen, with filtering capabilities.
    
*   **🔧 Flexible Configuration:** All settings are managed via environment variables for easy integration into containerized and cloud environments.
    
*   **🚀 Production-Ready:** Includes guidance for deployment using a production-grade WSGI server like Gunicorn.
    

Requirements
------------

*   Python 3.8+
    
*   A running **Redis Server** instance
    
*   Required Python packages, which can be installed from requirements.txt.
    

Installation
------------

1.  Bashgit clone cd
    
2.  bleachFlaskgunicornlxmlredisrequestssqlparse
    
3.  Bashpip install -r requirements.txt
    
4.  **Ensure Redis is running** and accessible from where you are running the WAF.
    

Configuration
-------------

MaxWAF is configured entirely through environment variables. You can set them in your terminal, a .env file, or your deployment environment.

VariableDescriptionDefaultREAL\_APP\_HOSTThe hostname or IP of your backend web application.localhostREAL\_APP\_PORTThe port your backend web application is running on.80REDIS\_HOSTThe hostname or IP of your Redis server.localhostREDIS\_PORTThe port your Redis server is running on.6379RATE\_LIMIT\_COUNTMax requests per IP within the time window.100RATE\_LIMIT\_WINDOWThe time window for rate limiting, in seconds.60BAN\_DURATIONHow long an IP is banned after hitting the BAN\_SCORE\_THRESHOLD, in seconds.300THREAT\_SCORE\_THRESHOLDA request with a score above this will be **blocked** (403).15BAN\_SCORE\_THRESHOLDA request with a score above this will cause the source IP to be **banned**.25WAF\_MODESet to passthrough to disable all security checks for benchmarking.enforcingExport to Sheets

Running the WAF
---------------

Bash

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   redis-server   `

**Run the Logger Service (in a separate terminal/process):**

Bash

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   python logger.py   `
