## Secure your Application Code from Vulnerabilities and Errors with Code Scanning 🛡️

### What is Code Scanning🛡️?

***Code scanning is a feature by GitHub that will scan your repositories for vulnerabilities and errors in your code. It will scan for vulnerabilities like SQL Injection, Cross-Site Scripting(XSS), etc. and errors like unused variables, etc. It will also prevent developers from pushing code that contains vulnerabilities and errors.We can also Schedule the scanning process to run at a specific time, events like Pull Request, push, etc. Code scanning will scan your code and notify you about the vulnerabilities and errors in your code.***

### How does Code Scanning work?

Code Scanning uses `CodeQL` behind the scenes to scan our code. CodeQL is the code analysis engine developed by GitHub to automate security checks. Code Scanning uses CodeQL to scan the code and will display the alerts in the `Code Scanning Alerts` tab of the repository. 

We know that Code Scanning uses CodeQL to scan the code. But how does CodeQL work? CodeQL uses GitHub Actions behind the Scenes to scan the code.
Once Code Scanning gets enabled for the repository, According to the schedule, Code Scanning will run the CodeQL analysis with GitHub Actions and will display the alerts in the `Code Scanning Alerts` tab of the repository.


### Who can use this feature?

Code Scanning is available for all public repositories. Fior private repositories, Code Scanning is available for Organizations that have GitHub Enterprise Cloud and have GitHub Advanced Security.

### Sample Code for Code Scanning

I have created a sample repository called `gh-advanced-security` and I am going to push the below code that contains a vulnerability to the repository and will enable Code Scanning for the repository. Let's see how Code Scanning works.

```python
# I got this code from ChatGPT for demonstrating Code Scanning, Don't use this code in your Production or any other Environments.

import sqlite3
import os
import hashlib

# Vulnerability 1: SQL Injection
# Just Triggering again
def get_user_info(user_id):
    conn = sqlite3.connect('example.db')
    cursor = conn.cursor()
    # Unsafe query vulnerable to SQL injection
    query = f"SELECT * FROM users WHERE id = {user_id};"
    cursor.execute(query)
    result = cursor.fetchone()
    conn.close()
    return result

# Vulnerability 2: Insecure use of eval()
def calculate_expression(expression):
    # Using eval is dangerous and can execute arbitrary code
    result = eval(expression)
    return result

# Vulnerability 3: Hardcoded sensitive data
def get_secret_key():
    # Sensitive data should not be hardcoded in the source code
    secret_key = "super_secret_key_123"
    return secret_key

# Example usage
if __name__ == "__main__":
    user_id = input("Enter the user ID: ")
    user_info = get_user_info(user_id)
    print(f"User Info: {user_info}")

    expression = input("Enter a mathematical expression to calculate: ")
    result = calculate_expression(expression)
    print(f"Result: {result}")

    secret_key = get_secret_key()
    print(f"Secret Key: {secret_key}")
```

### How to enable Code Scanning?

Before enabling Code Scanning, we need to understand what are the options available for Code Scanning. There are two options available for Code Scanning. They are:

1. Default: In this option, GitHub will use the default Code Scanning configuration to scan the code. GitHub will automatically choose the best configuration as per the language used in the repository.

2. Advanced: In this option, we can customize the Code Scanning configuration as per our requirements. The Code scanning config file will be stored in the `.github/workflows` directory of the repository.

To enable Code Scanning for the repository, Follow the below steps:


Once enabled, You have to wait for GitHub actions to run and Complete


Now navigate to `Security` tab of your repository and then `Code Scanning Alerts` to view the alerts. You can see the alerts like below:



### Closing the Alert


You can react to the alert by either creating an issue or fixing the vulnerability. If you want to create an issue, you can click on the `Create Issue` button and create an issue. Or you can fix the vulnerability yourself. It's up to you. Once you fix the vulnerability, you can close the alert by clicking on the `Dismiss Alert` button. In my Case this alert is not a valid one, so I am going to close it by choosing the `False Positive` option. Once you click on the `Close Alert` button, the alert will be closed and you can see the alert status as `Closed`.

You can also add more tools to you Code Scanning workflow by clicking on the `Add tools` button. It will take you to the `Actions` tab of your repository and you can add more tools to your Code Scanning workflow.

### Disabling Code Scanning

You can disable Code Scanning for your repository by following the below steps:

1. Navigate to the repository settings.
2. Click on the `Code security and analysis` tab.
3. If you scroll down, you can see the `Code scanning` section.
4. Click on the `...` button and then click on the `Disable CodeQL` button to disable Code Scanning for your repository.

For more information on Code Scanning, you can refer to the [official documentation](https://docs.github.com/en/code-security/code-scanning).