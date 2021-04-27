## Single Sign On (SSO)

If you wish to integrate our closed user group portal/site with your own applications and user group, you can utilize our SSO functionality.

Process: 

1. [Request a Site Admin](mailto:hello@hotelsforhope.com?Subject=Request%20for%20Site%20Admin%20User) to be added to your closed user group site (if you don't already have one)
2. Get a token for the Site Admin
3. Create a member using the Site Admin's token
4. Use the member's token in queries on the user's behalf

<aside class="notice">
If you use our portal's UI and wanted to link directly to a particuilar page without requiring login, use the parameter `memberToken={MEMBER-TOKEN}` in the URL (replacing <code>{MEMBER-TOKEN}</code> with the browsing user's token).
</aside>
