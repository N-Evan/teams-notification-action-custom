# MS Teams PR Notification

This GitHub Action helps you automatically send notifications to Microsoft Teams when pull requests events occur such as opened, reopened or synced. Customize your notifications with configurable themes, titles, and images to keep your team informed about new code changes directly in your Teams channel.

Features:
- Easy integration with Microsoft Teams
- Customizable notification appearance
- Supports all GitHub-hosted runners
- Minimal setup required

Streamline your code review process and enhance team collaboration with real-time pull request updates in Microsoft Teams.

## Inputs

| Input Name     | Description                                        | Required | Default Value |
|----------------|----------------------------------------------------|----------|---------------|
| `webhook_url`  | Microsoft Teams webhook URL                        | Yes      | N/A           |
| `pr_title`     | Title of the pull request                          | Yes      | N/A           |
| `pr_url`       | URL of the pull request                            | Yes      | N/A           |
| `pr_creator`   | Creator of the pull request                        | Yes      | N/A           |
| `repo_name`    | Name of the repository                             | Yes      | N/A           |
| `theme_color`  | Theme color for the Teams message card (hex code)  | No       | `0076D7`      |
| `custom_title` | Custom title for the Teams message card            | No       | (Empty)       |
| `activity_image`| URL of the custom activity image                  | No       | GitHub Logo   |

## Example Usage

To use this action, define it in your workflow YAML file like so:

```yaml
name: PR Notification

on:
  pull_request:
    types: [opened, reopened]

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: MS Teams PR Notification
        uses: haroldelopez/ms-teams-notification-action@v1.0.0
        with:
          webhook_url: ${{ secrets.TEAMS_WEBHOOK_URL }}
          pr_title: ${{ github.event.pull_request.title }}
          pr_url: ${{ github.event.pull_request.html_url }}
          pr_creator: ${{ github.event.pull_request.user.login }}
          repo_name: ${{ github.repository }}
```

## Customization
You can customize the notification by adding optional inputs:

```yaml
- name: Send Teams Notification
  uses: haroldelopez/ms-teams-notification-action@v1.0.0
  with:
    webhook_url: ${{ secrets.MS_TEAMS_WEBHOOK_URL }}
    pr_title: ${{ github.event.pull_request.title }}
    pr_url: ${{ github.event.pull_request.html_url }}
    pr_creator: ${{ github.event.pull_request.user.login }}
    repo_name: ${{ github.repository }}
    theme_color: '00FF00'
    custom_title: 'New PR Alert!'
    activity_image: 'https://example.com/custom-image.png'
```

- Theme Color: You can customize the theme_color input to change the appearance of the message card in Microsoft Teams. This should be a hex code (e.g., FF5733).

- Custom Title: If you'd like to use a different title for the Teams message card, set the custom_title input. Otherwise, the pull request title will be used.

- Activity Image: You can change the image in the notification by providing a custom URL for activity_image.

## Required Permissions
Ensure that the repository has access to the necessary secrets:

- TEAMS_WEBHOOK_URL: The Microsoft Teams webhook URL should be stored as a repository secret.

## Troubleshooting
The action will fail if any of the required inputs (webhook_url, pr_title, pr_url, pr_creator, repo_name) are missing.
Make sure the webhook URL is correctly configured and accessible.

## License
This project is licensed under the MIT License - see the LICENSE file for details.

## Contributing
Contributions are welcome! Please feel free to submit a Pull Request.

## Support
If you encounter any problems or have any questions, please open an issue in this repository.
