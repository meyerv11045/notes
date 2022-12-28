# Cloud Stuff



## Training Notifications

- [Source](https://towardsdatascience.com/how-to-get-a-notification-when-your-training-is-complete-with-python-2d39679d5f0f)
- hard to get knockknock working on a linux VM right now b/c keyring is tough to get setup
- Get emails when training starts, finishes, &/or crashes

``` python
from knockknock import email_sender

@email_sender(recipient_emails=["vjmeyer20@gmail.com", "vikram.j.meyer@vanderbilt.edu"], sender_email="trainstatus88@gmail.com")
def train():
	...

if __name__ == '__main__':
    train()
```

- [set app password for logging in from yagmail](https://myaccount.google.com/u/2/apppasswords?rapt=AEjHL4PQcBhs-VEwMdDnP1Z3cYGnNOD7Y8MBdUCeMky5r2uWNBCxtcYTUFgv6VZSkUmPbrFfy3eUBZyHXVDdBH9ZkFl10_6Sfw)
- [how to reset saved keyring password for knockknock](https://stackoverflow.com/questions/63971590/how-to-reset-the-keyring-of-stored-email-password-in-visual-studio-code-in-windo)



