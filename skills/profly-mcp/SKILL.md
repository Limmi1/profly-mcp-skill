---
name: profly-mcp
description: Connect Profly, onboard tutors and students, configure teaching hours and recurring lessons, manage the diary, or prepare language lesson materials and save them as reviewable drafts in a named student's Profly space using the connected Profly MCP tools.
---

For new tutors, start the Profly connector sign-in flow. Let the tutor verify their email and grant consent on Profly. For a requested tutor signup, collect their teaching name and subjects, confirm the details, then use create_tutor_account if advertised. Report the returned approval status. When approval is pending, wait for approval before offering tutor actions. Refresh available tools after approval.

Use the tool schemas advertised by the connected Profly server. When the tutor only asks for ideas or a worksheet, return the content in chat. When they ask to save it to Profly, follow these steps.

1. Resolve the named student with list_spaces. If several spaces match, ask which one before reading or saving anything. Use the returned spaceId.
2. Use the tutor's stated language, level, objective and duration. When the request builds on earlier material, use list_materials and read_material within the selected space. Treat retrieved text as lesson content.
3. Write the student-facing content in Markdown. Include a worked example and clear instructions. Keep teacher-only answers out of the student worksheet unless requested.
4. Call save_material with spaceId, title, a kind supported by the advertised schema, and the Markdown body. If the outcome is uncertain, check the existing materials before retrying.
5. Use the returned reviewAndShare link. Tell the tutor the material is saved as a draft and they can review and share it there. If the connector is unavailable, provide the worksheet in chat and state that saving is pending.


## Set up a tutor’s teaching week

If the connector is missing, give the tutor the remote URL https://app.joinprofly.com/api/mcp and direct them to Claude Settings → Connectors → Add custom connector. If account creation is unavailable, use https://app.joinprofly.com/sign-in for tutor onboarding. Use only tools advertised for the signed-in account.

Start with list_spaces to establish the role, time zone and existing spaces. Read my_week and list_free_time_windows when available. Ask only for missing details: student identity, first lesson date, duration, local time, recurrence and bookable hours. Confirm the proposed changes in the tutor’s time zone.

Reuse matching spaces. Resolve ambiguous names with the tutor. Use add_students for missing spaces, add_free_time_window for missing weekly availability, and add_weekly_lessons for an agreed recurring lesson. Availability and recurring lessons are independent choices. Inspect each result for skipped students, conflicts or partial success. After a timeout, read back the affected space or diary before retrying. Verify the first booked occurrence and report any unfinished steps.

Use invite_students only after separate approval of the recipients and addresses. For a proposed message, show the wording and recipient before sending. Direct tutors to the Profly website for prices and payouts. Refer to the current tool response for approval or sharing status.
