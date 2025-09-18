So we have this problem at work where we need to share sensitive stuff like API keys, passwords, or access tokens with team members but only temporarily. Right now people either use LastPass (which doesn't really do temp sharing well) or worse, they just dump it in Slack which is terrible for security.

What we need is something in between - a secure vault specifically for temporary sharing. The idea is you can create a secure link to share a secret, and that link has limits - maybe it can only be accessed 3 times, or it expires after 24 hours, whatever you set. Once those conditions are met, poof, the data is gone. No more "hey I shared that password 6 months ago in Slack, let me scroll back forever to find it" situations.

The system should have its own user management but keep it simple - anyone with a company email (like @deriv.com for us) can register. They signup and set their password. We'll need some basic admin functionality too, where admins can manage users, deactivate accounts if someone leaves, that sort of thing. But here's the important part - even admins shouldn't be able to see the actual secrets. The whole point is security, so no backdoors.

We will keep the list of users and audit logs in a single Postgres Database. Keep it simple. one single DB a few tables. When users create a secret they set which of current users will be able to see the secret and they will get a link. Links Themselves alone are not enough to reveal the secret.

Secrets will be stored encrypted and with TTL in Redis.

Key things we care about:
- Encrypted storage obviously, following security best practices
- Links that self-destruct after X views or Y time
- Audit logs so we know who accessed what and when
- Support for different types of secrets (passwords, files, multi-line text like certificates)
- Clean simple interface, nothing fancy, just secure and reliable

This isn't meant to replace our main password manager, it's specifically for those "hey can you share the staging DB password real quick" situations. Make it dead simple to use but impossible to mess up security-wise.