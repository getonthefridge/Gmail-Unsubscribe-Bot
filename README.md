![CodeRabbit Pull Request Reviews](https://img.shields.io/coderabbit/prs/github/getonthefridge/Gmail-Unsubscribe-Bot?labelColor=171717&color=FF570A&link=https%3A%2F%2Fcoderabbit.ai&label=CodeRabbit%20Reviews)

# Unsubscribing from Junk Emails using Gmail API

## Overview
This program connects to a Gmail account, retrieves recent emails, identifies junk email subscriptions, and attempts to unsubscribe from them automatically.

## Pseudocode

```plaintext

# Authenticate with Gmail API
FUNCTION authenticate_gmail():
    LOAD credentials from OAuth2.0 JSON file
    BUILD Gmail API service
    RETURN authenticated service object

# Fetch recent emails
FUNCTION get_recent_emails(service, max_results):
    CALL Gmail API to fetch latest emails (max_results limit)
    RETURN list of email messages

# Extract unsubscribe links from emails
FUNCTION extract_unsubscribe_links(email_messages):
    INITIALIZE empty list unsubscribe_links
    FOR each email in email_messages:
        PARSE email headers for "List-Unsubscribe" field
        IF "List-Unsubscribe" field exists:
            EXTRACT and STORE unsubscribe link
    RETURN unsubscribe_links

# Unsubscribe using extracted links
FUNCTION unsubscribe_from_links(unsubscribe_links):
    FOR each link in unsubscribe_links:
        SEND HTTP request to the unsubscribe link
        LOG success or failure

# Move identified junk emails to spam
FUNCTION mark_as_spam(service, email_messages):
    FOR each email in email_messages identified as junk:
        CALL Gmail API to move the email to spam

# Main execution
CALL authenticate_gmail() -> service
CALL get_recent_emails(service, max_results=50) -> emails
CALL extract_unsubscribe_links(emails) -> unsubscribe_links
CALL unsubscribe_from_links(unsubscribe_links)
CALL mark_as_spam(service, emails)

```
