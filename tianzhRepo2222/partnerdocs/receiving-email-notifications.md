# Receiving email notifications from Open Publishing

To receive email notifications from the Open Publishing Build Service, you need to modify some of your personal account settings on GitHub.

Click the profile drop-down in the upper right and choose **Settings**. 

## To get email for push operations:

1. Go to the **Emails** tab in the left nav.
2. Clear the **Keep my email address private** checkbox.
    
    When this option is unchecked and you push commits, GitHub sends OP a notification with the primary email address in this list.  Otherwise, GitHub sends OP a notification with *username*@users.noreply.github.com, and you won't receive a notification from OP.

## To get email for pull requests:

1. Go to the **Profile** tab in the left nav.
2. Set a public email.

    For a pull request, GitHub does not send OP the user's email address.  So OP looks up the username to get the user's public email address, which is listed in this field.  If you don't list one, you won't get mail for your pull request.

