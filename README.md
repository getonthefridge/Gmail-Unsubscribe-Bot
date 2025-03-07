# Gmail-Unsubscribe-Bot

Pseudocode for Unsubscribing from Junk Emails using Gmail API



DEFINE function authenticate_gmail()
    LOAD credentials from OAuth2.0 JSON file
    BUILD Gmail API service
    RETURN authenticated service object

DEFINE function get_recent_emails(service, max_results)
    CALL Gmail API to fetch latest emails (max_results limit)
    RETURN list of email messages

DEFINE function extract_unsubscribe_links(email_messages)
    INITIALIZE empty list unsubscribe_links
    FOR each email in email_messages
        PARSE email headers for "List-Unsubscribe" field
        IF "List-Unsubscribe" field exists
            EXTRACT and STORE unsubscribe link
    RETURN unsubscribe_links

DEFINE function unsubscribe_from_links(unsubscribe_links)
    FOR each link in unsubscribe_links
        SEND HTTP request to the unsubscribe link
        LOG success or failure

DEFINE function mark_as_spam(service, email_messages)
    FOR each email in email_messages identified as junk
        CALL Gmail API to move the email to spam

# Main execution
CALL authenticate_gmail() -> service
CALL get_recent_emails(service, max_results=50) -> emails
CALL extract_unsubscribe_links(emails) -> unsubscribe_links
CALL unsubscribe_from_links(unsubscribe_links)
CALL mark_as_spam(service, emails)

END
