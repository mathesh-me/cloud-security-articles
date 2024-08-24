## Secure your Application Code with Secret Scanning

### What is Secret Scanning?

***Secret scanning is a feature by GitHub that will scan your repositories for exposed secrets. In this case, secrets means some sensitive information like API keys, passwords, and tokens. When these secrets are exposed, it may lead to unauthorized access to your application or data. So, we need to secure our application code by not exposing these secrets in repositories.***

Let's say by mistake you or your team member pushed a code that contains a secret key. GitHub will scan your repository in real-time and notify you about the exposed secret. So that you can take action immediately. By default secret scanning is enabled for all public repositories. Not available for private repositories.

### How does Secret Scanning work?

**Secret scanning works by scanning the repositories for exposed secrets using some particular patterns. By pattern I mean, some specific format that a secret key follows**. For example, an AWS Access Key and Secret Key follows a specific pattern. So, if GitHub finds a pattern that matches with the secret key during the scanning process, it will notify you about the exposed secret immediately.<br>

Also, there is a concept called Secret Scanning Partner program. GitHub has partnered with some service providers to scan for their secrets. When a secret is exposed, GitHub will notify the service provider about the exposed secret to take actions such as revoking the secret key. For example, if you are using AWS, GitHub will scan your repository for AWS secrets using the AWS secret scanning partner program.

### How to enable Secret Scanning?

As I mentioned earlier, secret scanning is enabled by default for all public repositories. For Private repositories, you can't enable secret scanning(I read some articles from GitHub and didn't found anything for Private Repositories, If you find any, Please create a PR with the Reference Link). Once enabled, GitHub will scan your private repositories for exposed secrets and notify you about the exposed secrets immediately.

### Triggering Secret Scanning

For this demo, I created one public repository called `gh-advanced-security` and I am going to push some code that contains a secret key to the repository.<br>
Let's push some code that contains a secret key to the repository. I have one sample file called `alertmanager.yml` that contains Slack webhook URL. If you don't know what `alertmanager.yml` is, it is a configuration file for the Alertmanager tool. Alertmanager is a tool that is used to send alerts to different platforms like Slack, Email, etc. and it requires a webhook URL to send alerts to Slack. Here `Webhook URL` is the secret key that we need to secure. You can assume the `Webhook URL` is equivalent to the AWS Access Key and Secret Key.

Let's push this file to the repository and see how secret scanning works.

```yaml
global:
  slack_api_url: 'https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX'
route:
  # The below receiver is a Default receiver. If the alert doesn't match any of the receivers in routes section, It will send the alert to the default receiver.
  receiver: 'slack-notifications'
  # To send alerts to different receivers based on different conditions, We can use the "routes" section.
  # routes:
  #   - match:
  #       severity: critical
  #     receiver: 'slack-notifications'
  #   - match:
  #       severity: warning
  #     receiver: 'slack-notifications'
  
receivers:
  - name: 'slack-notifications'
    slack_configs:
      - send_resolved: true
        channel: '#channel_name'
        icon_emjoi: ':warning:'
```

Once you push the code, GitHub will scan the repository for exposed secrets and notify you about the exposed secret. In this case, it will notify you about the exposed Slack webhook URL.<br>

If you navigate to the repository security tab, you can see the exposed secret by following the steps below:


You will also get notified about the exposed secret via email. The email will contain the exposed secret and the repository name. You can take action immediately to secure your application code.

You can also close this once you took action on the exposed secret. In my case the URL is not valid, so I am going to mark this as false positive and close it. You can close the alert by clicking on the `close as` button.

You can even apply some filters to the secret scanning alerts. For example, you can filter the alerts based on the secret type, repository, or the secret itself.

### Disabling Secret Scanning

If you want to disable secret scanning for your public repository, then follow the steps below:

1. Navigate to the repository settings.
2. Click on the `Code security and analysis` tab.
3. If you scroll down, you can see the `Secret scanning` section.
4. Click on the `Disable` button to disable secret scanning for your repository.

### Available Advanced Security Features for you GitHub Account

Follow the below steps to check the available advanced security features for your GitHub account:

