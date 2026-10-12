# Security considerations and hardening roadmap

## Current safeguards
- Read-only account for Wazuh alert retrieval.
- SSH tunnel for Indexer access.
- Backend-only handling of Indexer credentials.
- Safe DOM text insertion with `textContent`.
- No router port forwarding required for phone demonstration.

## Known risks
1. **Unauthenticated Flask dashboard on LAN:** Other devices with network reachability may access camera footage and events. Return to loopback binding when not demonstrating; add login/authentication and HTTPS before regular use.
2. **Development server:** Flask's built-in server is not intended as a hardened production deployment. Use an appropriate deployment stack when ready.
3. **Indexer TLS verification disabled:** Temporary `verify=False` accepts certificates without verification. Configure the proper CA trust chain and certificate name verification.
4. **Biometric privacy:** Recognition models and camera footage are sensitive; use consented subjects, short retention, encryption, and access controls.
5. **False positives:** Unknown-face alerts indicate a model classification, not a verified threat.
6. **Secrets in Git:** Review Git history and working tree before publishing; `.gitignore` does not protect secrets already committed.

## Release gate before public hosting
- [ ] Login and session protection
- [ ] HTTPS end-to-end
- [ ] Verified Indexer TLS certificate
- [ ] No secrets in repository or Git history
- [ ] Secure retention and privacy policy
- [ ] Access logging and basic rate limiting
- [ ] Test failure modes and error handling
