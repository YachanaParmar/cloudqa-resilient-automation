# Resilient CloudQA Form Automation

A C# Selenium WebDriver project that tests three fields on the CloudQA Automation Practice Form:

- First Name
- Gender
- State

## Technology

- C#
- .NET 8
- Selenium WebDriver
- Google Chrome

## Approach

The project uses a semantic element resolver rather than relying exclusively on fixed CSS selectors or XPath expressions.

It identifies form elements using:

- Associated labels
- ARIA attributes
- Nearby field and group labels
- Placeholder text
- Element types
- HTML attributes as secondary evidence

Candidates are scored for relevance. When multiple candidates have nearly identical scores, the resolver reports ambiguity rather than silently selecting the first match.

## Running the Project

Requirements:

- .NET 8 SDK
- Google Chrome

Build:

    dotnet build src/CloudQa.Automation/CloudQa.Automation.csproj

Run:

    dotnet run --project src/CloudQa.Automation

Custom URL:

    dotnet run --project src/CloudQa.Automation -- --url "https://example.com/form"

Custom values:

    dotnet run --project src/CloudQa.Automation -- --first-name "Alex" --gender "Female" --state "India"

Headless mode:

    dotnet run --project src/CloudQa.Automation -- --headless

## Verification

The project has been manually tested against:

1. Original CloudQA practice form.
2. A modified form with reordered elements.
3. Modified IDs and names.
4. Additional HTML wrappers.
5. A similar-looking Billing First Name field.
6. Duplicate Guardian Gender and applicant Gender groups.

The duplicate-group test also verified that the applicant's Female option was selected.

Local mutation fixtures are included in the tests directory.

## Important Note

The CloudQA field labeled State currently contains country names in the observed page. The default test value is India.

## Limitations

- Identical controls with indistinguishable semantic context may be ambiguous.
- The current implementation targets native HTML form controls.
- Significant changes to the form's semantic structure may require additional handling.
- Mutation checks were run manually; they are not yet an automated regression suite.

## Test Result

The original page and the tested mutation fixtures passed during local development.
