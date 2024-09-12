# Securing Application Code from Vulnerabilities and Attacks with DependaBot

We know how important it is to keep our application code up-to-date by updating packages and dependencies. But managing this process manually can be time-consuming and error-prone. We have to check the package versions, look for security advisories, and then update the packages accordingly. This is where Dependabot comes in. Dependabot is a GitHub tool that will automates the process of checking for outdated packages and dependencies in your codebase and creating pull requests to update them. In this article, we will see how to set up Dependabot for your GitHub repository and secure your application code from vulnerabilities and attacks.

## What is Dependabot?

**Dependabot is a GitHub tool that helps us to keep our packages and dependencies up-to-date by automatically creating pull requests to update them.** It will checks for outdated packages and dependencies in our code and then creates pull requests to update them.

## Who can use Dependabot?

Dependabot alerts are free to use for all repositories on GitHub. Advanced capabilities, like the ability to create custom auto-triage rules for Dependabot alerts, are available (for free) on public repositories only.

## Setting up Dependabot

To set up Dependabot for your GitHub repository, follow these steps:

Already I have a repository named `gh-advanced-security` in my GitHub account. This is the repository that I used for demonstration purposes of GitHub Advanced Security features. Now I will set up Dependabot for this repository.

### Pushing Vulnerable Package Versions to the Repository


Now, I am going to push some files with Vulnerable Package versions to the repository. I have created a files named `app.py` and `requirements.txt` with vulnerable package versions. I will push these files to the repository.

```python
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

You can see that I have used vulnerable package versions in the `requirements.txt` file and Pushed these files to the repository. But there is no Dependabot alerts created for these vulnerable package versions till now. This is because Dependabot is not enabled for this repository. Now I will enable Dependabot for this repository.

### Enabling Dependabot Alerts

To enable Dependabot alerts for your repository, follow these steps:

You can see there are five options to enable Dependabot alerts for the repository. You can choose the option that suits your needs. I am going to enable the first two options to enable Dependabot alerts for this repository and it will also create a pull request to update the packages to the latest versions. Also note that If you enable `Dependabot security updates` option, Dependabot will automatically enable the last option that is `Dependabot on Actions Runners` because behind the scenes Dependabot uses GitHub Actions to create pull requests to update the packages.
// Images will be added here


You can also Check the `Actions` tab in the repository to see the Dependabot actions that are running to check for outdated packages and dependencies in the code and creating pull requests to update them.


Now you can once we enable Dependabot alerts for the repository, it will start checking for outdated packages and dependencies in the codebase and create pull requests to update them. You can see I got a Dependabot alert for the vulnerable package versions that I pushed to the repository. Dependabot has created a pull request to update the packages to the latest versions.

### Dependabot Pull Request

You can see that Dependabot has created a pull request to update the packages to the latest versions. You can review the changes and merge the pull request to update the packages.

Now I am going to merge this pull requests to update the packages to the latest versions.

### Disabling Dependabot Alerts

To disable Dependabot alerts for your repository, follow these steps:

// Images will be added here

Now you can see that I have disabled Dependabot alerts for the repository. Once we disable Dependabot alerts, it will stop checking for outdated packages and dependencies in the codebase and creating pull requests to update them.