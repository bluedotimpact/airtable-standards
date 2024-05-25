# BlueDot Impact Airtable Standards

These are standards to improve the maintainability of large Airtable databases (similar to coding standards for programming languages).

Jump to:
- [Bases](#bases)
- [Tables](#tables)
- [Collaborative views and locked views](#collaborative-views-and-locked-views)
- [Fields](#fields)
- [Automations](#automations)
- [Extensions](#extensions)
- [External apps](#external-apps)
- [Structured description](#structured-description)
- [Standard prefixes](#standard-prefixes)

## Motivation

At BlueDot Impact we manage a large number of Airtable bases.

These bases used to be a mess. From one of our internal documents before implementing the standards:

> Our Airtable is messy, which makes discovering, syncing and using data much harder than it needs to be. It also risks us making mistakes by misinterpreting data, as well as holding data for unnecessarily long. This is already slowing us down and causing problems, and is a key blocker in us continuing to innovate.

Since implementing these standards, our bases are much easier to navigate, making it much faster to find necessary information. It's also significantly reduced the number of errors we make in our bases, and has sped up the development of further applications on top of our Airtable.

We believe you can (and probably should) implement these standards too. We've been told by multiple Airtable staff and expert Airtable consultants that we have by far some of the most advanced systems built on Airtable they've ever seen, so reckon if this works for us it can work for you.

## How to use these standards

The key words "must", "must not", "required", "should", "should not", "recommended", "may", and "optional" in this document are to be interpreted as described in [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119).

Toggle blocks are used only to provide additional explanation or clarification.

_Organisation_ refers to the organisation adopting these standards (e.g. BlueDot Impact).

## Scope

<ul><li><details>
<summary>All workspaces, bases, tables, collaborative views, locked views, automations, extensions and fields that <i>Organisation</i>'s staff are primarily responsible for maintaining (including everything in the <i>Organisaton</i>'s Airtable account) must comply with these standards.</summary>

- This intentionally excludes personal views to allow people to do whatever they like in a scratch space, with minimal overhead. These sometimes eventually become collaborative views - when this happens then the standards would apply to them.
</details></li></ul>

- **Exception:** tables, views, automations, extensions and fields do not need to comply with the standards if they are inside bases which:
  - were created in the last 3 months, and:
    - aren’t expected to be used after 1 month from now; or
    - are planned to be made compliant with the standards within 1 month
  - (for the avoidance of doubt: the base still needs to comply with the base standards)

## Bases

<ul><li><details>
<summary><b>Required:</b> Store bases containing non-mock data in an enterprise workspace in the <i>Organisation</i>'s Airtable account</summary>

- Clarification: Non-mock data is any data that is ‘real’, for example real information about our users, our staff, our curriculums, our websites etc. This is as opposed to mock data, which is stuff like test users (e.g. ‘Mr Test Test’ with email ‘test@gmail.com’).
- Why: This ensures we have oversight over what data we hold, and we’re able to review things like sharing and syncs more easily. It also allows others to discover the base more easily (but you may change the sharing settings to disallow access if necessary).
</details></li></ul>

<ul><li><details>
<summary><b>Recommended:</b> Store bases in an enterprise workspace in the <i>Organisation</i>'s Airtable account</summary>

- Why: This allows others to discover the base more easily, and facilitates better hand-overs etc. as these bases are available to others.
- Why might you not do this: Bases with solely mock data where we need to give lots of people builder/contributor access e.g. the Work Trials base. This is because we may want to exclude this from our enterprise workspaces to reduce costs (workspaces and bases are free on enterprise, costs come from each additional “builder/contributor”).
</details></li></ul>

<ul><li><details>
<summary><b>Required:</b> Name your base in <a href="https://en.wikipedia.org/wiki/Letter_case#Sentence_case">sentence case</a> (first letter and names capitalised), avoiding punctuation if possible. The name should make it clear what the base’s purpose is / what it likely holds. If you have bases for different <a href="https://en.wikipedia.org/wiki/Deployment_environment#Environments">environments</a>, prefix them with this e.g. <code>[prod]</code>, <code>[dev]</code>, <code>[local]</code>.</summary>

- Example: `Applications`, `Course builder`, `[prod] Time availability forms`
</details></li></ul>

<ul><li><details>
<summary><b>Recommended:</b> Merge bases that contain similar entities.</summary>

- What: For example, don't create 'Alignment course builder' and 'Governance course builder' bases - just create one 'Course builder' base.
- Why: This reduces confusion, makes it easier to maintain data integrity, and makes it easier to build apps that work across the same types of things (e.g. multiple courses).
</details></li></ul>

- **Required:** Add a [Structured description](#structured-description) to the base guide:
  - Required: Owner
  - Required if custom prefixes used in base: Prefixes
  - Recommended: Description
  - Required: Last reviewed on
  - Optional: Consider deletion on
  - Example:
    ```
    Owner: alice@bluedot.org
    Prefixes:
    [a] Data directly from the applicant
    [e] Data from an evaluator
    Description: This base is for applications and evaluations for courses run by BlueDot Impact ourselves.
    Last reviewed on: 2023-08-07
    ```
- **Recommended:** If using field prefixes, try to make them obvious without having to look at the documentation. Try to be consistent with them across bases.
  - Example: prefer ‘[connect]’ over ‘[c]’
  - Example: rather than using all of ‘[connect]’, ‘[agisc]’, ‘[agsc]’, and ‘[c]’, pick one and stick to it

## Tables

<ul><li><details>
<summary><b>Required:</b> Name your tables in <a href="https://en.wikipedia.org/wiki/Letter_case#Sentence_case">sentence case</a> without punctuation. The table should be named after what each record represents in the table, which means it will usually be singular.</summary>

- Example: `Applicant`, `Class reading`
- Example (should be noun):<br/>
  `Monster fighting` → `Monster fight`
- Example (should represent thing):<br/>
  `Fight feedback form` → `Fight feedback` or `Fight feedback form submission`<br/>
  (if each row represents a piece of feedback from the form, rather than a form itself)
- Example (should normally be singular):<br/>
  `evaluations` → `evaluation` (if each row is a single evaluation)
- Example where plurals are right:<br/>
  `user_preferences` (if each row contains all the preferences for the user)
- Why noun: Consistent table naming makes it easier to skim the names of tables and know what is in them.
- Why singular: We use the singular because it works with other tools more intuitively (like Bubble or SQL, e.g. ‘Find an Activities’ vs ‘Find an Activity’), makes naming relations between data easier (e.g. join tables, or relations that are already plural). These are not super important reasons, but we should be consistent throughout and it seems like the reasons lean singular. Also see:
  - https://www.teamten.com/lawrence/programming/use-singular-nouns-for-database-table-names.html
  - https://dba.stackexchange.com/questions/13730/plural-vs-singular-table-name
  - https://www.clearlyagile.com/agile-blog/singular-table-name-convention-in-entity-framework-core-v2
</details></li></ul>

<ul><li><details>
<summary><b>Required:</b> Merge tables in the same base that represent the same entity.</summary>

- What: For example, don't create 'Alignment applicants' and 'Governance applicants' tables - just create one 'Applicants' table.
- Why: This reduces confusion, makes it easier to maintain data integrity, and makes it easier to build apps that work across the same types of things (e.g. multiple courses).
</details></li></ul>

- **Required:** Add a [Structured description](#structured-description) to the table:
  - <details><summary>Optional: Owner</summary><ul><li>This should be added if you are creating a table, and you are not the owner of the base.</li><li>Prefer to omit this if the same as the owner of the base, and it’s expected to be this way into the future. Why: reduces amount to have to migrate over and potential for things getting out of sync when transferring parent ownership.</li></ul></details>
  - Recommended: Description
  - Required: Last reviewed on
  - Optional: Consider deletion on
  - Example:
    ```
    Owner: alice@bluedot.org
    Description: Evaluations for the July 2023 AI Governance course, held for data analysis.
    Last reviewed on: 2023-08-07
    Consider deletion on: 2023-10-01
    ```

## Collaborative views and locked views

- **Required:** The view that shows all fields without filters/grouping should be called ‘All’. There must not be a view called ‘All’ that is not this.
- **Required (Optional for ‘All’ view):** Add a [structured description](#structured-description) to the view:
  - Required: Owner
  - Recommended: Description
  - Required: Last reviewed on
  - Optional: Consider deletion on
  - Example:
    ```
    Owner: alice@bluedot.org
    Description: Undergrad applicants who we’re most unsure about accepting to the AI governance course.*
    Last reviewed on: 2023-08-07
    ```
<ul><li><details>
<summary><b>Required:</b> If the view is shared with or synced to another base or service, lock the view.</summary>

- Why: This prevents accidental changes from breaking our automations or syncs.
</details></li></ul>

<ul><li><details>
<summary><b>Required:</b> If the view is shared with or synced to another service (e.g. Make.com, Zapier, Whalesync, Bubble, custom app), add information about where it syncs in the description, ideally with a link to that location.</summary>

- Why: This prevents accidental changes from breaking our automations or syncs.
</details></li></ul>

<ul><li><details>
<summary><b>Required:</b> If the view is shared outside of _Organisation_ (e.g. the public, employers, people running our courses), lock the view.</summary>

- Why: This prevents accidental information disclosure, by reducing the risk of making filters more permissive or adding more columns accidentally
</details></li></ul>

- **Recommended:** Group related views using sections for better organization.

## Fields

- Naming
  - <details><summary><b>Required:</b> Name your field in <a href="https://en.wikipedia.org/wiki/Letter_case#Sentence_case">sentence case</a>, without punctuation except for prefixes. It should be clear from the table context, the name and field type what the field means (further clarification can be given in the description).</summary><ul><li>Example: <code>First name</code>, <code>Class readings</code>, <code>[connect] Is email public</code>, <code>[>] Overall recommendation</code></li><li>Why: Consistent field naming makes it easier to skim the names of fields, and makes it less likely that they are changed to something that breaks existing automations or integrations.</li></ul></details>
  - <details><summary><b>Recommended:</b> Date fields should end in `on`, date-time fields should end in `at`, boolean fields should start with `Is`. Avoid naming fields like this that aren’t these types.</summary><ul><li>Example: <code>Next bank holiday on</code>, <code>Created at</code>, <code>Is reading completed</code></li><li>Why: Consistent field naming makes it easier to skim the names of fields, and hint at the type of fields from their names alone.</li></ul></details>
  - <details><summary><b>Required:</b> Don’t repeat the table name in the title.</summary><ul><li>Example: <code>Applicant first name</code> should be just <code>First name</code> in the <code>Applicant</code> table</li></ul></details>
  - <details><summary><b>Required:</b> Prefix fields with relevant <a href="#standard-prefixes">standard prefixes</a>.</summary><ul><li>Why: Standard prefixes exist to make it clearer when fields behave a certain way. For example, that people should be aware it’s linked to automations, or that it’s a lookup or derived field so users know the original source data is coming from somewhere else.</li><li>Example: <code>[>] Overall recommendation</code><br/>This could be the field in the applicant table that shows linked evaluations’ overall yes/no/maybe recommendations.</li><li>Example: <code>[>] [*] Evaluation average total score</code><br/>This could be the field in the applicant table that shows the average of linked evaluations’ total scores.</li></ul></details>
  - <details><summary><b>Optional:</b> Prefix fields with prefixes defined in the base guide.</summary><ul><li>Example: <code>[connect] Is email public</code></li><li>Why: This helps group and organize related fields.</li></ul></details>
- <details><summary><b>Required:</b> Use the native number, date, time, and checkbox types rather than treating them as text.</summary><ul><li>Why: This ensures that the data is entered correctly and can be easily sorted, filtered, and analyzed.</li></ul></details>
- <details><summary><b>Required:</b> Do not include leading or trailing slashes on URLs or URL fragments, unless it is a final URL (i.e. won’t be concatenated with anything else) AND is required for the URL to work correctly.</summary><ul><li>Example (no trailing slash, URL):<br/><code>https://google.com/</code> → <code>https://google.com</code></li><li>Example (no leading or trailing slash, URL fragment):<br/><code>/courses/ai-governance/</code> → <code>courses/ai-governance</code></li><li>Why: Overall, having consistent URL formatting makes it easier for us to make assumptions about how to handle URLs. The actual way round is less justified, but vaguely:<ul><li>From a very small sample, it appears that many big websites appear to prefer no trailing slash on full URLs (Google, YouTube, Facebook, Microsoft, LinkedIn, Twitter)</li><li>Our own course hub breaks with extra trailing slashes: so enforcing links ending in slashes might then cause difficulties if we're not concatenating things on (e.g. https://course.aisafetyfundamentals.com/governance/)</li><li>Tools for building URLs tend to expect the origin and fragments not to include slashes themselves (e.g. JavaScript URL, Node.js path.join, Java URL)</li></ul></li></ul></details>
- <details><summary><b>Required:</b> Use ISO format for the date part of date-time fields.</summary><ul><li>How: Right click the field > Edit field > Formatting > Date format</li><li>Why: This reduces ambiguity and confusion because by default Airtable shows dates in ‘Local’ (which means American) format: which is unnatural to most of us in the UK.</li></ul></details>
- <details><summary><b>Recommended:</b> Use date-time fields rather than date fields where possible.</summary><ul><li>Why: This gives us more granular data, and using the same field types across the board makes it easier to transition automations etc. between fields. This is also often useful for figuring out how recently a dataset was updated (e.g. ‘sometime today’ vs ‘2 minutes ago’ is useful to know), as well as inferring properties of applications (e.g. two applications in the same minute = likely duplicate, two applications on the same day 20 hours apart = likely trying to add additional info)</li></ul></details>
- <details><summary><b>Recommended:</b> Use a unique, human-usable primary key</summary><ul><li>How: If there isn’t one nice field that can be used as a primary key, consider using a formula field as the primary key. For example, you could concatenating fields to form something unique, or even include the Airtable record id in the primary key (however, to keep it human-usuable usually don’t *just* use the record id).</li><li>Why: This makes it easier to find and distinguish records in surfaces where only the primary key is presented (e.g. interfaces, linked records), reducing the chance of errors due to selecting the wrong item. It also makes building automations that join things on primary keys more reliable, especially syncs across bases.</li></ul></details>
- **Recommended:** Add a [structured description](#structured-description) to the field:
  - <details><summary>Optional: Owner</summary><ul><li>This should be added if you are creating a field, and you are not the owner of the table.</li><li>Prefer to omit this if the same as the owner of the base, and it’s expected to be this way into the future. Why: reduces amount to have to migrate over and potential for things getting out of sync when transferring parent ownership.</li></ul></details>
  - Recommended: Description
  - Recommended: Last reviewed on
  - Optional: Consider deletion on
  - If indefinite, prefer explicitly entering ‘Forever’
  - Example:
    ```
    Owner: alice@bluedot.org
    Description: Whether the applicant is okay with us sharing their data with our partners to offer them further study opportunities and jobs.
    Last reviewed on: 2023-08-07
    ```
- <details><summary><b>Recommended:</b> Avoid pulling many lookup fields from another table. Try to use link fields instead. If you need to see all this information at the same time, consider building an interface for this rather than using many lookups.</summary><ul><li>Why: Lookup fields can clutter tables with data that’s not really relevant to them, which can cause confusion when interpreting them and make it harder to find information relevant to just the specific entity. It can also be confusing where fields are being pulled in from.</li></ul></details>

## Automations

- **Required:** Give your automation a name that at least roughly explains what it does, and group related automations to make it easier to navigate.
- **Recommended:** Give your automation a description that explains what problem it aims to solve, and why it is built the way that it is. Include instructions on how to use the automation. Optionally, this could be through an interface with clear usage instructions and details about what the automation will do (e.g. maybe with a live preview).

<ul><li><details>
<summary><b>Required:</b> Use comments as necessary in custom scripts so it would be clear to someone familiar with Airtable scripting what the script is doing and why it’s doing it.</summary>

- This doesn’t mean you have to comment everything, or explain things that are just part of the coding language (as long as they aren’t too exotic or weird). This is more intended to answer questions like ‘it’s sending this data to some webhook: but what is that webhook linked to / do’ or ‘it’s updating these records, but why is that even necessary’
</details></li></ul>

## Extensions

- **Required:** Give your extension a name that at least roughly explains what it does.

## External apps

- <details><summary><b>Recommended:</b> Use field ids, rather than field names to reference fields.</summary><ul><li>Why: This makes apps less fragile to renaming fields.</li><li>How: For TypeScript applications, use <a href="https://github.com/domdomegg/airtable-ts">airtable-ts</a>.</li></ul></details>

## Structured description

You can [add descriptions](https://support.airtable.com/docs/adding-descriptions-in-airtable#adding-and-viewing-descriptions-in-airtable) to Airtable bases, tables, views, fields, automations, extensions and workspaces.

A structured description is a format for writing descriptions so that they are easily human and machine readable. This allows us to have consistency in how we label things so it’s easy to understand, and in future will enable us to build automations that read the descriptions to review things (e.g. highlight areas with unclear ownership, flag when we still have columns that no longer need to be retained). For example:

```
Owner: alice@bluedot.org
Prefixes:
- [app] Information from their application
- [connect] Information relating to AIS Connect
Description: This base is for applications and evaluations after May 2023 for internally-run BlueDot Impact courses.
Last reviewed on: 2023-08-07
Consider deletion on: 2023-09-01
```

The format is a series of key-value pairs, each separated by a colon (`:`). The values of pairs may flow onto multiple lines. New pairs must be on a new line. Blank lines are ignored.

Keys:

- Owner: The owner of the entity, who is responsible for maintaining it. Inherits from the parent (e.g. table owner defaults to the base owner). Format: a single email, usually at _Organisation_'s domain.
- Prefixes: A list of common prefixes used in the base, excluding [standard prefixes](#standard-prefixes). Format: Line-separated rows of a dash bullet, square brackets encasing the prefix, and then a description.
- Description: An accurate explanation of the scope and purpose of the entity. If the entity is shared or synced to a third party service (like Bubble), the description should explain what it is shared to and why. Format: free text.
- Last reviewed on: When the entity was last looked at and reconsidered by the owner (e.g. description updated and considered still relevant). Format: A date in YYYY-MM-DD format.
- Consider deletion on: When the entity is likely to no longer be useful and should be reviewed for deletion, in consultation with the entity owner. Format: A date in YYYY-MM-DD format, or not declared (assumed to be never).

The keys that are required and allowed for each type of Airtable infrastructure is explained its corresponding section.

## Standard prefixes

Prefixes are used to group associated fields or highlight common meanings about fields. The following are prefixes used across bases that don’t need to be defined in the base structured description:

- `[!]`: Trigger for an automation (e.g. ‘Send email’)
- `[?]`: Confirmation that an automation has been completed, written to by the automation - also to prevent infinite loops (e.g. ‘Is email sent’)
- `[>]`: A field that is a lookup or link to another table
- `[*]`: A field that is derived from others, e.g. a formula or rollup
- `[tmp]`: A temporary field that can be immediately deleted after immediate use (e.g. expected to live less than 1 day)

If using multiple standard prefixes, place them in the order they are in the list (e.g. `[!]` before `[>]`).
