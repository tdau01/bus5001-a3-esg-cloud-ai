# Q1 GreenDesk Test Log

- Agent: GreenDesk ESG Assistant (Dialogflow CX, australia-southeast1)
- Tested in the Dialogflow CX simulator and saved test cases
- Same content as Appendix A of the report

| Test | Input sequence | Result |
|---|---|---|
| T01 | hi -> I want to report a water leak -> Building C, level 2 kitchen -> medium -> yes | Pass: summary shown, logged for Facilities Maintenance |
| T02 | report an issue -> someone dumped chemicals in the bin -> Science building, lab 4 -> low | Pass: escalated (hazardous even at low urgency) |
| T03 | there's a leak in the library -> Library level 1, near the stairs -> it's flooding, critical | Pass: escalated |
| T04a | the wheelchair ramp is blocked | Fail: not recognised. Fixed by adding synonyms |
| T04b | ... high -> change -> waste contamination -> Building B cafe -> low -> yes please | Pass: answers cleared, logged for Sustainability Office |
| T04c | Retest: the wheelchair ramp is blocked | Pass |
| T05 | what's the weather today? | Pass: Start Page no-match message |
| T06 | report an issue -> actually, cancel my report | Pass: cancelled |
| T07a | the lights are left on all night | Fail: not recognised. Fixed with training phrases and synonyms |
| T07b | lights left on -> Building D level 3 offices -> not sure -> medium -> yes | Pass: severity reprompt, logged for Facilities Maintenance |
| T08 | ... -> talk to a person (at the urgency step) | Pass: escalated |
| T09a | there's a water leak -> talk to a person (at the location step) | Fail: saved as the location |
| T09b | Retest after page-level human.agent route | Fail: @sys.any still captured it |
| T09c | Retest after condition route: can I talk to a real person? | Pass: escalated |
| T10 | Regression: there's a water leak -> Building C, level 2 kitchen -> low | Pass: summary shown |
| T11 | report an issue -> banana -> banana -> banana (15 Oct) | Pass: two reprompts, then hand-off to Escalate |
| T12a | hi -> I want to talk to human (15 Oct) | Fail: no-match message. Fixed by adding training phrases to human.agent |
| T12b | Retest: hi -> I want to talk to human | Pass: escalated |
| Suite | T01 to T12 saved as test cases and run on Draft (15 Oct) | 12 of 12 passed |
