# Security Best Practices (for Prompting)

> **Library:** Prompt Engineering Template Collection
> **Author:** Deb Barman
> **Template ID:** PTL-40

---

## 01. Overview

Security Best Practices is a meta-level template — rather than describing a technique for producing a creative or technical deliverable, it describes how to prompt safely: what not to put in a prompt, how to request security-conscious output from a model, and how to structure prompts that will be used in production or automated systems so they resist misuse. This template covers both directions of the security concern: protecting sensitive information from being exposed to or through a model, and requesting that generated code/content itself follows secure practices.

## 02. Purpose

- Prevent sensitive data (credentials, personal information, proprietary information) from being included in prompts unnecessarily.
- Ensure generated code follows secure coding practices by default, not as an afterthought.
- Structure prompts used in production/automated systems to resist prompt injection and misuse.
- Build awareness of what should never appear in a prompt, regardless of the task.

## 03. Use Cases

- Requesting code that must follow secure coding practices (input validation, auth handling, secrets management)
- Structuring prompts for production systems that process user-provided input
- Reviewing existing code or systems for security issues
- Sanitizing example data before including it in a prompt
- Building prompt templates that will be reused with variable, potentially untrusted input

## 04. Target AI Models

- ChatGPT (GPT-4, GPT-4o, GPT-4.1, and later)
- Claude (all Claude models)
- Gemini
- Grok
- Perplexity (relevant for security research context)

## 05. Prompt Category

`Meta-Level` · `Security` · `Best Practices`

## 06. Difficulty Level

**Intermediate to Advanced**

## 07. Required Inputs

- **Task**: The underlying request (code, review, system design)
- **Security requirements**: What security properties matter for this specific task

## 08. Optional Inputs

- Threat model / concerns specific to the context
- Compliance requirements (data handling standards relevant to the context)
- Whether the prompt itself will process untrusted/variable input

## 09. Variables

| Variable | Required? |
|---|---|
| `{{task_description}}` | Yes |
| `{{security_requirements}}` | Yes |
| `{{threat_model}}` | No |
| `{{compliance_requirements}}` | No |
| `{{untrusted_input_handling}}` | No |

## 10. Prompt Template

```text
Complete the following task with security as an explicit requirement, not
an afterthought.

TASK:
{{task_description}}

SECURITY REQUIREMENTS:
{{security_requirements}}

RELEVANT THREAT MODEL / CONCERNS:
{{threat_model}}

COMPLIANCE REQUIREMENTS (if applicable):
{{compliance_requirements}}

IF THIS PROMPT/SYSTEM WILL PROCESS UNTRUSTED INPUT:
{{untrusted_input_handling}}

INSTRUCTIONS:
- Apply standard secure-by-default practices even if not every one is
  explicitly listed above: validate and sanitize input, avoid hardcoded
  secrets, use parameterized queries (never string-concatenated SQL），
  apply least-privilege access, and handle errors without leaking
  sensitive internal details.
- Explicitly note any security trade-off being made and why, rather than
  silently choosing convenience over a more secure approach.
- If the task as described would require handling genuinely sensitive data
  (credentials, personal data, payment info), flag the specific handling
  requirements relevant to that data type.
- Do not include real credentials, API keys, personal data, or other
  sensitive values in example code or output — use clearly-marked
  placeholders instead.
```

## 11. Placeholder Explanation

| Variable | Description | Example |
|----------|-------------|----------|
| `{{task_description}}` | The underlying task | "Write an API endpoint that accepts a user-submitted search query" |
| `{{security_requirements}}` | Specific properties needed | "Must prevent SQL injection; must rate-limit per user" |
| `{{threat_model}}` | Relevant attack surface | "Endpoint is public-facing, unauthenticated users can submit queries" |
| `{{compliance_requirements}}` | Applicable standards | "Must not log full query text if it could contain PII" |
| `{{untrusted_input_handling}}` | How variable input is treated | "Treat all query parameters as untrusted; validate type and length before use" |

## 12. Example Input

```text
TASK: Write a Node.js/Express endpoint that accepts a username and password
for login and checks them against a database.

SECURITY REQUIREMENTS: Prevent SQL injection, prevent timing attacks on
password comparison, no plaintext password storage/comparison

THREAT MODEL: Public-facing login endpoint, will receive automated
credential-stuffing attempts

UNTRUSTED INPUT: Treat username and password fields as fully untrusted;
validate presence and reasonable length before processing
```

## 13. Example Output

```javascript
const bcrypt = require("bcrypt");
const rateLimit = require("express-rate-limit");

// Rate limiting to reduce automated credential-stuffing risk
const loginLimiter = rateLimit({
  windowMs: 15 * 60 * 1000,
  max: 5,
  message: "Too many login attempts, please try again later.",
});

app.post("/login", loginLimiter, async (req, res) => {
  const { username, password } = req.body;

  // Basic input validation before any processing
  if (
    typeof username !== "string" ||
    typeof password !== "string" ||
    username.length === 0 ||
    username.length > 254 ||
    password.length === 0
  ) {
    return res.status(400).json({ error: "Invalid request" });
  }

  try {
    // Parameterized query — prevents SQL injection
    const result = await db.query(
      "SELECT id, password_hash FROM users WHERE username = $1",
      [username]
    );

    // Generic error message regardless of whether username exists,
    // to avoid leaking which usernames are valid
    if (result.rows.length === 0) {
      // Still run a bcrypt compare against a dummy hash to keep timing
      // consistent whether or not the username exists
      await bcrypt.compare(password, "$2b$10$invalidsaltinvalidsaltinvalidsa");
      return res.status(401).json({ error: "Invalid credentials" });
    }

    const user = result.rows[0];
    const passwordMatches = await bcrypt.compare(password, user.password_hash);

    if (!passwordMatches) {
      return res.status(401).json({ error: "Invalid credentials" });
    }

    // Issue session/token here (implementation depends on your auth strategy)
    return res.status(200).json({ message: "Login successful" });
  } catch (err) {
    // Log the real error internally; never expose internal details to the client
    console.error("Login error:", err);
    return res.status(500).json({ error: "An error occurred" });
  }
});
```

```text
SECURITY NOTES:
- Parameterized query used throughout — no string concatenation of user
  input into SQL.
- bcrypt.compare() used for password checking instead of plaintext or
  simple hash comparison, since bcrypt is designed to be slow (resisting
  brute force) and its compare function is timing-attack resistant.
- A dummy bcrypt comparison runs even when the username isn't found, to
  keep response timing consistent and avoid leaking username validity
  through timing differences.
- Generic error messages returned to the client either way, avoiding
  username enumeration.
- Rate limiting applied at the route level to reduce credential-stuffing
  effectiveness.
- Real errors logged server-side only; the client never sees internal
  error details.
```

## 14. Customization Guide

- **State the actual threat model, not just "make it secure"**: A public-facing endpoint and an internal admin tool have very different realistic threats — naming the actual exposure (public/authenticated/internal) helps the model apply proportionate, relevant protections.
- **Name specific compliance requirements when they apply**: General "handle data securely" is vague; specific requirements (e.g., not logging PII, data residency, retention limits) should be stated explicitly since they vary significantly by context and jurisdiction.
- **Always mark untrusted input explicitly**: Any prompt template that will later be filled with real user input should explicitly instruct that such input is untrusted, especially for prompts used in automated/production systems.
- **Use placeholders for anything sensitive, always**: Never include real credentials, API keys, or personal data in a prompt — even for a one-off example, use clearly fake or placeholder values.

## 15. Output Format Options

- Code block + security notes
- Checklist (for security review tasks)
- Table (for comparing security trade-offs of different approaches)
- Markdown (for security documentation/guidelines)

## 16. Best Practices

- Explicitly request security-by-default practices rather than assuming they'll be applied without being asked.
- State the actual threat model/exposure level so protections are proportionate and relevant, not generic.
- Always use placeholder values for anything sensitive — never include real secrets, credentials, or personal data in a prompt, even temporarily.
- Request explicit flagging of any security trade-off made for convenience, so it's a visible decision rather than a silent one.

## 17. Common Mistakes

- Including real credentials, API keys, or personal data in a prompt "just for this example" — treat every prompt as potentially logged/stored.
- Requesting code without any security requirements, then discovering vulnerabilities (SQL injection, hardcoded secrets, missing input validation) only later.
- Not specifying the threat model, resulting in generic security advice that may not address the actual realistic risk for that specific context.
- Assuming a single security review or generated implementation is sufficient without human security review for anything genuinely high-stakes (authentication, payment processing, PII handling).

## 18. Prompt Variations

- **Basic Version**: Task + general "make it secure" instruction, no specific requirements.
- **Advanced Version**: Full structure with specific security requirements, threat model, and untrusted input handling (Section 10).
- **Expert Version**: Adds a request for the model to also list what it did NOT address (e.g., "this covers input validation and injection prevention but does not address rate-limiting infrastructure or WAF configuration, which should be handled at the infrastructure level") — making the boundary of what was actually covered explicit.

## 19. Related Prompts

- `21_Code_Generation_Prompts.md` — this template's security requirements should typically be layered into code generation requests by default for anything handling real data or public exposure
- `22_Debugging_Prompts.md` — security-focused debugging (investigating a potential vulnerability) follows similar root-cause-first principles
- `19_Function_Calling.md` — schema validation for function calls is itself a security-relevant practice (preventing malformed or malicious input from reaching downstream systems)

## 20. Tips

- For any prompt template that will be reused with real user input (a customer support bot, a search feature), explicitly testing the template with deliberately adversarial or malformed input examples before deployment is a valuable practice — it surfaces prompt injection or unexpected-behavior risks early.
- Treat "the model wrote secure-looking code" as a strong starting point, not a final security guarantee — genuinely sensitive systems (authentication, payments, access control) warrant human security review and, where appropriate, professional penetration testing in addition to careful prompting.

## 21. Limitations

- Generated code and security guidance should not be treated as a substitute for a real security review, especially for systems handling authentication, payments, or sensitive personal data.
- Security best practices and known vulnerability patterns evolve; the model's knowledge reflects its training data and may not include the most recently discovered vulnerability classes or newly deprecated practices.
- This template addresses prompting practices and generated-content security; it does not cover broader infrastructure security (network configuration, server hardening, physical security) which requires separate expertise.

## 22. Model Compatibility

| Model | Supported |
|--------|-----------|
| ChatGPT | ✅ |
| Claude | ✅ |
| Gemini | ✅ |
| Grok | ✅ |
| Perplexity | ✅ (relevant for security research context) |
| Llama (open-source) | ✅ |
| Mistral | ✅ |

## 23. Tags

`#security` `#secure-coding` `#best-practices` `#advanced` `#meta-level`

## 24. Version History

| Version | Date | Changes |
|---|---|---|
| 1.0 | 2025 | Initial release |

## 25. License / Credits

Compiled by **Deb Barman** as part of the *Prompt Engineering Template Collection*.
Free to use, adapt, and share with attribution.
