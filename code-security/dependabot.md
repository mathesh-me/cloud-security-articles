# Protecting Your Code: How Dependabot Secures Applications from Vulnerabilities and Attacks

We know how important it is to keep our application dependencies up-to-date because outdated packages and dependencies can lead to security vulnerabilities and attacks. But updating dependencies manually can be time-consuming and error-prone. We have to check the package versions, look for security advisories, and then update the packages accordingly. This is where Dependabot comes in. `Dependabot` is a GitHub tool that will automates the process of checking for outdated packages and dependencies in your codebase and creating pull requests to update them. In this article, we will see how to set up Dependabot for your GitHub repository and secure your application code from vulnerabilities and attacks.

## What is Dependabot?

**`Dependabot` is a GitHub tool that helps us to keep our packages and dependencies up-to-date by automatically creating alerts and pull requests to update them.** It will checks for outdated packages and dependencies in our code and then creates pull requests to update them.

## Working Architecture

![Dependabot](https://github.com/user-attachments/assets/d35e2609-786d-4458-b4ad-197f1aff1788)

## Who can use Dependabot?

Dependabot alerts are free to use for all repositories on GitHub. Advanced capabilities, like the ability to create custom auto-triage rules for Dependabot alerts, are available (for free) on public repositories only.

## Setting up Dependabot

To set up Dependabot for your GitHub repository, follow these below mentioned steps:

For this demo, I have a repository named `gh-advanced-security` in my GitHub account. This is the repository that I used for demonstration purposes of GitHub Advanced Security features. Now I will set up Dependabot for this repository. In this repository you can also find guides for other GitHub Advanced security features like Code Scanning and Secret Scanning. You also need to create one if you don't have already.


![Screenshot 2024-09-09 220812](https://github.com/user-attachments/assets/47807865-93f5-4af1-922d-91dfe4d7acdb)


### 1. Pushing Vulnerable Package Versions to the Repository

Now, I am going to push some files with Vulnerable Package versions to the repository. I have created a files named `app.py` and `requirements.txt` with vulnerable package versions. These files are for simple Python application. I am going push these files to the repository now. Let's see what will happen


![Screenshot 2024-09-09 222903](https://github.com/user-attachments/assets/3c0c7840-bcd2-45af-9183-92ae09cff82c)


![Screenshot 2024-09-09 223002](https://github.com/user-attachments/assets/8b59d8db-737c-400f-8911-f4256511b018)



```python
# app.py
from flask import Flask, jsonify
import requests

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello, It's a sample app!"

@app.route('/api')
def get_api_data():
    try:
        response = requests.get("https://jsonplaceholder.typicode.com/todos/1")
        data = response.json()
        return jsonify(data), 200
    except Exception as e:
        return jsonify({"error": str(e)}), 500

if __name__ == '__main__':
    app.run(debug=True)
```

```python
# requirements.txt
flask==2.2.5  # Known vulnerability in Flask < 1.0
requests==2.32.2  # Known vulnerability in requests < 2.20.0
```

Here you can see I have used vulnerable package versions in the `requirements.txt` file and Pushed these files to the repository. But there is no Dependabot alerts created yet for these vulnerable package versions. This is because Dependabot is not enabled for my repository till now. Let's enable Dependabot for this repository.


![Screenshot 2024-09-09 223024](https://github.com/user-attachments/assets/b841337b-006b-402c-b35d-faae52f8581d)


### 2. Enabling Dependabot Alerts

To enable Dependabot alerts for your repository, follow these steps:


![Screenshot 2024-09-09 223034](https://github.com/user-attachments/assets/c441e441-8e3d-4061-abf0-eadb843a808e)


![Screenshot 2024-09-09 223134](https://github.com/user-attachments/assets/41d0d447-c9c1-42c4-83f3-74cf5a8093ce)


As shown above there are five options to enable Dependabot alerts for the repository. Each have it's own feature, you can choose the option that suits your needs. I am going to enable the first two options to enable Dependabot alerts for this repository. First option is used to create alerts and the second option is for automatically creating pull requests to update the packages to the latest versions. Also note that If you enable `Dependabot security updates` option, Dependabot will automatically enable the last option that is `Dependabot on Actions Runners` because behind the scenes Dependabot uses GitHub Actions to create pull requests to update the packages.


![Screenshot 2024-09-09 223134](https://github.com/user-attachments/assets/a69628b8-9214-4780-aeef-cd38cbc0a241)


You can also Check out the `Actions` tab in the repository to see the Dependabot actions that are running to check for outdated packages and dependencies in the code and creating pull requests to update them.


![Screenshot 2024-09-09 223251](https://github.com/user-attachments/assets/2317662e-3059-4cf0-9680-89fff07d371f)


**Let's explore the alerts section**


![Screenshot 2024-09-09 223218](https://github.com/user-attachments/assets/706dbf10-3902-4665-ac6f-ef0d741a0dbe)


![Screenshot 2024-09-09 223236](https://github.com/user-attachments/assets/8c8b48ae-2a32-409d-a86f-a3860e27c8ba)


Once we enable Dependabot alerts for the repository, it will start checking for outdated packages and dependencies in the codebase and create pull requests to update them. You can see I got a Dependabot alert for the vulnerable package versions that I pushed to the repository. Dependabot has created a pull request to update the packages to the latest versions.

### 3. Merging Dependabot Pull Request

Dependabot has created a pull request already to update the packages to the latest versions. Now I am going to merge this Pull requests to update the package versions in my `requirements.txt` file


![Screenshot 2024-09-09 223305](https://github.com/user-attachments/assets/a76e85b8-fce4-4a81-bc2a-df29fcc0f4e8)


![Screenshot 2024-09-09 223327](https://github.com/user-attachments/assets/2542be86-05b2-415b-b43a-980a9005e0c2)


![Screenshot 2024-09-09 223604](https://github.com/user-attachments/assets/c07097c4-393a-44dc-889c-9ce2e73dfe93)


Here you can see my package versions got updated


![Screenshot 2024-09-09 223712](https://github.com/user-attachments/assets/8e5c5b0b-0ff9-46a8-8efe-b48f9db2cff6)


### 4. Disabling Dependabot Alerts

To disable Dependabot alerts for your repository, follow these steps:


![Screenshot 2024-09-09 223749](https://github.com/user-attachments/assets/08175644-cf4f-4920-a23b-ae90fdfa740a)


![Screenshot 2024-09-09 225004](https://github.com/user-attachments/assets/a78d5bc2-60c9-4c0f-a6f2-425f1ca32508)

Now you can see that I have disabled Dependabot alerts for the repository. Once we disable Dependabot alerts, it will stop checking for outdated packages and dependencies in the codebase and creating pull requests to update them.


For more information on Dependabot, you can refer to the official documentation [here](https://docs.github.com/en/code-security/supply-chain-security/keeping-your-dependencies-updated-automatically/about-dependabot-version-updates).