# PRD: CBE Event History and Schedule Tool

**Status:** Rough draft (week 4). Written before meeting the client. Sources: the week 4 lecture and two sample schedules (2021 EEC/Summit in Austin, 2018 Richland class session). Items marked *(assumption)* need to be checked with the client in week 5.

---

## Problem Statement

CBE runs executive education for the energy sector through three programs:

- The Energy Executive Course (EEC)
- The Energy Executive Summit
- The Legislative Energy Horizon Institute

Each event has a schedule and agenda: sessions, times, places, speakers and moderators. CBE has these documents for 2016 through 2026. Different people made them by hand over the years, so no two look alike. The two samples show how far apart they are:

- **The 2021 EEC/Summit schedule is a grid.** Days run across the top and times run down the side. Speakers are listed by name only, sometimes by last name only. Highlighting is the only thing showing which sessions the Summit participants also attended.
- **The 2018 Richland schedule is a list.** It goes day by day, and each line has a time and a session. Speakers are listed with their job title and organization. Classroom sessions are mixed in with bus times, meals, tours and hospitality suite hours.

Because the records are spread across files that don't match, CBE staff can't easily answer basic questions about their own history, such as "Has this person spoken for us before, and what was their role then?", "When did we last cover this topic?" or "Which organizations have we drawn speakers from?" Building a new event schedule also means copying from old documents rather than starting from organized data.

We are solving this for the CBE staff who plan and run these programs.

## Goals

Success means:

1. **All historical data in one place.** Every schedule from 2016 through 2026 is loaded into one organized collection with a single standard format, whatever its original layout.
2. **Fast lookup.** Staff can answer "has this person or organization been part of a past event?" in under a minute, without opening the original files.
3. **Staff can keep it current.** Staff can add, edit and delete records without technical help.
4. **Useful history.** Staff can see patterns across years and programs, such as repeat speakers, topics and organizations.
5. **Faster planning.** Staff can build a new event schedule using the tool.
6. **No data loss.** The data can be backed up and restored.
7. **Clean handoff.** At the end of the semester, CBE can run the product on its own.

## Constraints

- **Source layouts vary.** The files include grid-style and list-style Word documents, and possibly other formats. *(assumption)* The product has to bring all of them into one format.
- **Source detail varies.** Some schedules give a speaker's full name, title and organization. Others give only a name, or only a last name. The product can't require information the source doesn't have.
- **Some meaning lives only in formatting.** For example, highlighting marks the sessions shared with the Summit. That meaning must not be lost when the data is converted.
- **Public data only.** The event data is public, so there is no confidential information. Some documents include incidental contact details, such as staff phone numbers. The team will treat client material with discretion.
- **Non-technical users.** The people using it are event and program staff, not developers. *(assumption)*
- **Semester timeline.** The product has to be delivered and handed off to the client by the end of the semester.
- **Student team.** A team of four builds it, with AI assistance. Every change has to be approved by a teammate through a pull request.
- **Maintainability after handoff.** CBE has to be able to keep using the product after the student team is gone. *(assumption: CBE has little or no dedicated IT support)*

## Target Users / Personas

**1. Program Coordinator (primary user)**
Plans and runs one or more of the three programs. Builds agendas, invites speakers and moderators, and arranges site visits. Needs to know quickly who has spoken before, on what topic, in what role and when. Comfortable with office tools such as Word, but not with databases or code.

**2. Program Director / Leadership (secondary user)**
Oversees the programs and makes decisions about content and speakers. Mostly reads and analyzes rather than editing. Wants answers such as "How often do we repeat speakers?", "Which sectors are underrepresented?" or "How much do the EEC and Summit overlap?"

**3. Records Maintainer (occasional user)**
Whoever keeps the data accurate after handoff. Adds each new event's schedule, fixes errors and runs backups. May be the same person as the Program Coordinator. *(assumption)*

## User Stories

**Organized data and standard format**
- As a Program Coordinator, I want every past schedule in one standard format, whether it started as a grid or a list, so I can compare events across years and programs.
- As a Program Coordinator, I want a session shared by two programs (such as EEC and Summit) to show up under both, so neither program's history is incomplete.

**Add, edit and delete**
- As a Records Maintainer, I want to add a new event and its sessions after it's finalized so the history stays complete.
- As a Records Maintainer, I want to fix a misspelled name or fill in a missing title or organization so the records are accurate.
- As a Records Maintainer, I want to remove a session that was entered by mistake so it doesn't appear in searches or analysis.

**Search**
- As a Program Coordinator, I want to look up a person by name and see every session they took part in, as a speaker, panelist, moderator or faculty member.
- As a Program Coordinator, I want to search by organization so I can see everyone from that organization who has taken part.
- As a Program Coordinator, I want to search by topic or keyword (for example "Natural Gas" or "Smart Grid") so I can see when a subject was last covered.
- As a Program Coordinator, I want to filter by program, year and location so I can narrow my results.

**Analysis**
- As a Program Director, I want to see which people have taken part more than once, and in what roles.
- As a Program Director, I want to see which organizations and sectors are represented over time.
- As a Program Director, I want to compare topics covered across programs and years.

**Backup and restore**
- As a Records Maintainer, I want to back up all the data so a mistake or failure doesn't lose our history.
- As a Records Maintainer, I want to restore from a backup so I can recover from a bad edit or deletion.

**Build a new event schedule**
- As a Program Coordinator, I want to start a new event schedule with days, times, sessions, speakers and locations, and produce a finished schedule to share with participants.
- As a Program Coordinator, I want to see a person's past participation while I build a schedule so I can make informed choices.
- As a Program Coordinator, I want to start from a past event's schedule so I don't have to rebuild recurring items (meals, welcome, wrap-up) from scratch.

## Functional Requirements

Each requirement is written as a statement that can be tested.

**Data organization and standard format**
- FR-1: The system stores event records for all three programs from 2016 through 2026.
- FR-2: Every event record includes: program(s), year, start and end dates, city and main venue.
- FR-3: An event can belong to more than one program, and a single session can be marked as shared by more than one program.
- FR-4: An event can be one part of a larger class that meets several times in different places (for example, the 2018 Richland session followed by a DC session).
- FR-5: Every session record includes: date, start time, end time (where known), title, session type and location/room (where known).
- FR-6: Session type is one of a defined list, at minimum: presentation, panel, faculty course, exercise/case work, tour/site visit, meal or reception, and logistics. *(assumption: list to confirm with client)*
- FR-7: A session can list any number of people. Each person has a role in that session: speaker, panelist, moderator, faculty or host.
- FR-8: Every appearance records the person's title and organization *as of that event*, and allows them to be blank when the source doesn't give them.
- FR-9: The same person who appears at several events is recognized as one person, even if one source uses a full name and another uses only a last name. *(Open question: how the client defines "the same person")*
- FR-10: A session can have an optional sponsor (for example "Dinner sponsored by Dominion Energy").
- FR-11: All records follow one documented standard format no matter which source file they came from.
- FR-12: Each event record keeps a reference to the original source document it was converted from.

**Add, edit and delete**
- FR-13: A user can add a new event, session or person.
- FR-14: A user can edit any field of an existing record, and the change shows up in search and analysis right away.
- FR-15: A user can delete a record. The system asks for confirmation before deleting.
- FR-16: The system flags missing required fields when a record is saved.

**Search**
- FR-17: A user can search by person name and get every matching appearance across all programs and years, with the person's role in each session.
- FR-18: A user can search by organization, session title/topic keyword, program, year and location.
- FR-19: Name search returns matches despite small differences in spelling or formatting (for example "Bill Murray" vs. "William L. Murray"). *(assumption)*
- FR-20: Each search result shows the program, event, date, session title, and the person's role, title and organization at that time.
- FR-21: Users can choose to include or leave out logistics items (bus departures, hospitality suite hours) in search results.

**Analysis**
- FR-22: The system can list people who took part in more than one event, with a count and their roles.
- FR-23: The system can summarize participation by organization, program, year and session type.
- FR-24: The system can show which topics were covered in a given program or year range.

**Backup and restore**
- FR-25: A user can create a full backup of all data in one action.
- FR-26: A user can restore all data from a backup. Afterward the data matches the backup exactly.

**Build a new event schedule**
- FR-27: A user can create a new event schedule with days, sessions, times, locations, people and roles.
- FR-28: A user can copy a past event's schedule as the starting point for a new one.
- FR-29: A user can pull existing people from the historical records into a new schedule.
- FR-30: A user can export a completed schedule as a document to share with participants. *(assumption: format to confirm with client)*
- FR-31: A finished new schedule becomes part of the historical records.

## Out of Scope

Deferred to a later release, or not planned:

- Speaker invitations, emails or other communication with speakers or participants.
- Participant registration, ticketing, payments, budgeting or sponsorship tracking beyond recording a sponsor's name.
- Managing travel and logistics (buses, lodging, security badging). Logistics items may still be kept as schedule history, but the product won't manage them.
- A public-facing website or publishing agendas online.
- Data from before 2016, or from events outside the three named programs.
- Collecting data not in the source schedules (such as speaker bios, photos, contact details or session evaluations). *(to confirm with client)*
- Participant (attendee) records, such as class rosters or personal assessments.
- A mobile app.
- Integration with other CBE or university systems.

## Open Questions (for week 5)

- If a schedule gives only a last name, or a person's title and employer change between years, how does the client decide who is the same person?
- Should a person who was listed but didn't present (cancelled or replaced) count as a past speaker?
- Do logistics and social items (buses, meals, hospitality suites, tours) matter for search and analysis, or only as part of the full schedule?
- When a session is shared by the EEC and the Summit, which program does it belong to for reporting?
- How are multi-part classes (such as Richland followed by DC) related, and does the client think of them as one event or several?
- Who will maintain the data after handoff, and how comfortable are they with technical tools?
- What does a finished schedule need to look like when it's shared with participants? Is the grid or the list layout preferred?
