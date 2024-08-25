## Secure your Application Code from Vulnerabilities and Errors with Code Scanning 🛡️

### What is Code Scanning🛡️?

***Code scanning is a feature by GitHub that will scan your repositories for vulnerabilities and errors in your code. It will scan for vulnerabilities like SQL Injection, Cross-Site Scripting(XSS), etc. and errors like unused variables, etc. It will also prevent developers from pushing code that contains vulnerabilities and errors.We can also Schedule the scanning process to run at a specific time, events like Pull Request, push, etc. Code scanning will scan your code and notify you about the vulnerabilities and errors in your code.***

### How does Code Scanning work?

Code Scanning uses `CodeQL` behind the scenes to scan our code. CodeQL is the code analysis engine developed by GitHub to automate security checks. Code Scanning uses CodeQL to scan the code and will display the alerts in the `Code Scanning Alerts` tab of the repository. 

We know that Code Scanning uses CodeQL to scan the code. But how does CodeQL work? CodeQL uses GitHub Actions behind the Scenes to scan the code. Once Code Scanning gets enabled for the repository, According to the schedule, Code Scanning will run the CodeQL analysis with GitHub Actions and will display the alerts in the `Code Scanning Alerts` tab of the repository.

### Who can use this feature?

Code Scanning is available for all public repositories. For private repositories, Code Scanning is available for Organizations that have GitHub Enterprise Cloud and have GitHub Advanced Security.<br>

For Individual Accounts:

![Screenshot 2024-08-25 141106](https://github.com/user-attachments/assets/11991bd4-c532-413a-a6c6-ccfdea1321b0)

### Sample Code for Code Scanning

I have created a sample repository called `gh-advanced-security` and I am going to push the below code that contains a vulnerability to the repository and will enable Code Scanning for the repository. Let's see how Code Scanning works.

![Screenshot 2024-08-25 134834](https://github.com/user-attachments/assets/1471c592-14d1-4047-962e-9f06cd9b2727)

![Screenshot 2024-08-25 134850](https://github.com/user-attachments/assets/8e6b094c-b4b5-4040-a5cc-076ae899f896)

![Screenshot 2024-08-25 135235](https://github.com/user-attachments/assets/ace7dfbc-6a1b-49b6-9d80-79dfc8bc8e6e)

![Screenshot 2024-08-25 135304](https://github.com/user-attachments/assets/0155796c-64ff-4e75-aff2-98e6c30d8f8f)

Here is the Code I used:

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

1. **Default:** In this option, GitHub will use the default Code Scanning configuration to scan the code. GitHub will automatically choose the best configuration as per the language used in the repository.

2. **Advanced:** In this option, we can customize the Code Scanning configuration as per our requirements. The Code scanning config file will be stored in the `.github/workflows` directory of the repository.

To enable Code Scanning for the repository, Follow the below steps:

![Screenshot 2024-08-25 135324](https://github.com/user-attachments/assets/9f8f0302-d28d-403e-9d15-6b73f64c56a6)

![Screenshot 2024-08-25 135356](https://github.com/user-attachments/assets/ce413e50-95d7-4fae-8f99-47fa7a7797f0)

**If you choose advanced, You can Customize the CodeQL Configuration**
![Screenshot 2024-08-25 135411](https://github.com/user-attachments/assets/e0b12371-209c-426c-912b-b31e24b6b54d)

![Screenshot 2024-08-25 135430](https://github.com/user-attachments/assets/fa66e552-6b97-4277-9d2c-92493793574a)

**But for simplicity, I am going to start with Default Option**

![Screenshot 2024-08-25 135449](https://github.com/user-attachments/assets/47d13ebd-9ac5-4087-a2c4-27ed8c669634)

![Screenshot 2024-08-25 135512](https://github.com/user-attachments/assets/1ce75796-de4d-4478-802a-9a701ac5cf99)

**Once enabled, You have to wait for GitHub actions to run and Complete:<br>**

Navigate to `Actions` tab of your Respository

![Screenshot 2024-08-25 135556](https://github.com/user-attachments/assets/61f1317c-dc81-4519-8157-57b95c87d3c4)

![Screenshot 2024-08-25 135645](https://github.com/user-attachments/assets/373987c7-b5a4-4ee5-8676-8ea5a6e718dd)

![Screenshot 2024-08-25 135750](https://github.com/user-attachments/assets/468e62a7-a6ac-42a8-a3f4-7b858cf2eec3)

Now navigate to `Security` tab of your repository and then `Code Scanning Alerts` to view the alerts. You can see the alerts like below:

![Screenshot 2024-08-25 135804](https://github.com/user-attachments/assets/57f1aa84-3ce6-43b3-8157-f1a82da918b8)

You can also see the Severiry of Alert as `High`, `Low` or `Moderate` Labels

![Screenshot 2024-08-25 135813](https://github.com/user-attachments/assets/70e874e1-d027-4a0a-b0a8-6c6d80b25143)

![Screenshot 2024-08-25 135825](https://github.com/user-attachments/assets/dc946226-57ce-4877-820c-a6621679cd78)

### Closing the Alert

You can react to the alert by either creating an issue or fixing the vulnerability. If you want to create an issue, you can click on the `Create Issue` button and create an issue. Or you can fix the vulnerability yourself. It's up to you. Once you fix the vulnerability, you can close the alert by clicking on the `Dismiss Alert` button. In my Case this alert is not a valid one, so I am going to close it by choosing the `False Positive` option. Once you click on the `Close Alert` button, the alert will be closed and you can see the alert status as `Closed`.

![Screenshot 2024-08-25 135900](https://github.com/user-attachments/assets/b9e8c55c-fecc-4b57-a012-85554cc877f1)

Now, you can also add more tools to you Code Scanning workflow by clicking on the `Add tools` button. It will take you to the `Actions` tab of your repository and you can add more tools to your Code Scanning workflow.

![Screenshot 2024-08-25 135938](https://github.com/user-attachments/assets/97b97cc9-11a2-4c6c-ab72-36e57a0d26ca)

![Screenshot 2024-08-25 140006](https://github.com/user-attachments/assets/67b276a6-f8ca-471c-8410-efaa54351d76)

![Screenshot 2024-08-25 140020](https://github.com/user-attachments/assets/4d0dc05d-8d3d-4ac7-80a2-25ce429691ba)

![Screenshot 2024-08-25 140031](https://github.com/user-attachments/assets/e05ae736-9395-4f12-a02a-721c783b17be)


### Disabling Code Scanning

You can disable Code Scanning for your repository by following the below steps:

1. Navigate to the repository settings.
2. Click on the `Code security and analysis` tab.
3. If you scroll down, you can see the `Code scanning` section.
4. Click on the `...` button and then click on the `Disable CodeQL` button to disable Code Scanning for your repository.

### Third-Party Code Scanning Tools

We can also integrate third-party code scanning tools with GitHub Code Scanning. But the constraint is that the third-party code scanning tools should output Static Analysis Results Interchange Format (SARIF) data. SARIF is an open standard. We can run third-party analysis tools within GitHub using actions or within an external CI system.

**Note:** This is just a Introduction to Code Scanning. There is a lot we can do with Code Scanning like Customizing the Code Scanning Configuration, Adding more tools to the Code Scanning workflow, Using Third-Party Code Scanning tools, etc. If you want me to cover those topics, please let me know in LinkedIn or in Medium Page.

For more information on Code Scanning, you can refer to the [official documentation](https://docs.github.com/en/code-security/code-scanning).