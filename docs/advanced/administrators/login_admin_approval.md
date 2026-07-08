*Short version of this page:* 

**Admins** can go to [https://www.lambdafeedback.com](https://www.lambdafeedback.com), click 'Login with Microsoft', and **click approve**.

*Complete description:*

# Enabling single sign on

To login to Lambda Feedback with your organisation's Single-sign on requires approval from your organisation. Approval may be automatic, or may need to be given explicitly. This page contains instructions for organisations using a Microsoft login system ('Entra').

If users at your organisation see an **"Approval required"** screen when trying to sign in to Lambda Feedback, then explicit approval is required. This is a one-time step per organisation — once approved, all users can sign in without further prompts.

## App details

| Field | Value |
|---|---|
| Display name | Lambda Feedback Application |
| Application (client) ID | `ca92edb1-eb47-44b3-85a7-1011c51fb945` |
| Object ID | `4820f03e-b6be-4eb1-901a-46ed903b3de6` |
| Directory (tenant) ID | `2b897507-ee8c-4575-830b-4f8267c3d307` |

Use the **Application (client) ID** to confirm you're looking at the correct app if multiple results appear with similar names.

## Permissions requested

- **Sign in and read user profile**
- **Maintain access to data you have given it access to**

These are standard sign-in permissions and do not grant access to files, mail, or other organisational data.

## Who can approve this

You need one of the following Entra roles:

- Global Administrator
- Application Administrator
- Cloud Application Administrator

## How to approve

There are three alternative ways to approve - **any one** of them is sufficient:

### 1. Direct link

Admins for your organisation can login at 

[https://www.lambdafeedback.com](https://www.lambdafeedback.com)

and will see an option to approve.

### 2. Approve via a pending user request

If a user has already clicked **Request approval** on the consent screen, admins can approve their specific request:

1. Go to **Identity → Applications → Enterprise applications → Admin consent requests**
2. Find the pending request for **Lambda Feedback Application**
3. Review and approve it

This has the same effect as granting consent directly — all users are unblocked afterwards.

### 3. Go via the Entra admin center

1. Go to the [Microsoft Entra admin center](https://entra.microsoft.com)
2. Navigate to **Identity → Applications → Enterprise applications**
3. Search for **Lambda Feedback Application** (or paste the Application ID above into the search box to confirm the exact match)
4. Select the app, then open **Security → Permissions** (or just **Permissions**, depending on your tenant layout)
5. Click **Grant admin consent for [your organisation]**
6. Confirm the prompt

Once granted, this applies to **all users** in your organisation — no further requests will appear.

## Why does it say "unverified"?

Publisher verification is a separate, optional Microsoft process unrelated to the permissions themselves. An app can be fully legitimate without being publisher-verified. If you have questions about the app's security or maintainers, you can contact us for more details.

