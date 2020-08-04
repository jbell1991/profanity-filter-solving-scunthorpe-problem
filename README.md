# Problem to be Solved
For my Lambda Labs project, I was tasked with creating a profanity filter for a children’s reading app called Story Squad.  Story Squad prompts kids to read a new story or chapter of a book every week.  They then write their own creative story and draw a picture that branches off of that story.  The stories are handwritten to promote creativity from the students.  Their handwriting is read by the [Google Cloud Vision API](https://cloud.google.com/vision/?utm_source=google&utm_medium=cpc&utm_campaign=na-US-all-en-dr-bkws-all-all-trial-e-dr-1009135&utm_content=text-ad-none-any-DEV_c-CRE_291249276628-ADGP_Hybrid+%7C+AW+SEM+%7C+BKWS+%7C+US+%7C+en+%7C+EXA+~+ML/AI+~+Vision+API+~+Google+Cloud+Vision+Api-KWID_43700036257547156-kwd-475108777569&utm_term=KW_google%20cloud%20vision%20api-ST_Google+Cloud+Vision+Api&gclid=EAIaIQobChMI9PTkyvaB6wIVGey1Ch1p4gqpEAAYASAAEgJwjfD_BwE), which converts handwritten letters to typed text.  

Kids will be kids and from time to time inappropriate language might seep into the user experience.  Parents want to be able to trust their children are safe using the app.  However, we don’t want to deny stAnother problem with flagging profanity is that some words contain bad words within in them.  For example, the word “hell” is in “shell” and while hell would be deemed inappropriate for elementary students using the app, shell would not.  The problem is well-documented and is called the Scunthorpe Problem.  Scunthorpe is a town in England that contains a profane word.  A human would not make the mistake, but you could see how a computer might censor users from the town trying to set up an account on the web.  udents entry if their story was falsely flagged for profanity.  All stories are reviewed by human eyes to comply with the [Children’s Online Privacy Protection Rule](https://www.ftc.gov/enforcement/rules/rulemaking-regulatory-reform-proceedings/childrens-online-privacy-protection-rule) (“COPPA”), but we could prioritize stories to be reviewed by a moderator by flagging ones with profanity.  If a story is flagged, a moderator will review it before others and see if the flag is a true or false positive.  

# Scunthorpe Problem
Another problem with flagging profanity is that some words contain bad words within in them.  For example, the word “hell” is in “shell” and while hell would be deemed inappropriate for elementary students using the app, shell would not.  The problem is well-documented and is called the [Scunthorpe Problem](https://en.wikipedia.org/wiki/Scunthorpe_problem#:~:text=The%20Scunthorpe%20problem%20is%20the,obscene%20or%20otherwise%20unacceptable%20meaning.).  Scunthorpe is a town in England that contains a profane word.  A human would not make the mistake, but you could see how a computer might censor users from the town trying to set up an account on the web.  

# Options
One option explored was using python packages to find profanity.  Profanity-filter worked well on most words, but it still missed some individual words, missed phrases and did well to avoid flagging Scunthorpe like words.  

Another option was a package called profanity-check, which uses machine learning and not an explicit list of words to censor.  However, profanity-check failed to catch certain phrases.

The Story Squad stakeholder had a preference for flexibility in changing the list as slang changes.  Also, there are words that are inappropriate for elementary children that would not be considered inappropriate for adults.  These require a custom list of words.  

# Filter Using a Custom List of Bad Words
One problem with using a list is that whatever is not on the list will be missed, so the list has to be extensive.  The largest list of words I could find was a list of banned Google search terms consisting of ~1400 individual words and ~200 phrases to start.  

In my first iteration of the filter, the Scunthorpe Problem was apparent.  Because of the size of the list of words, many bad words were found nested inside of normal words.  Many false positives made for a poor filter and didn’t add value to the moderator.  

In the second iteration of the filter, the Scunthorpe Problem was solved by only flagging exact matches from the list.

# What can be improved?
In future iterations perhaps the filter could be used to flag if a child may be divulging personal information.  For example, a student writes a story and gives the name of their school or their address.  Words like school, elementary, middle, street, road, avenue etc. could be flagged for moderator review.  Again, the flexibility of using a custom list of words over machine learning is to flag items that aren’t necessarily offensive, but could still be harmful to children using the app.  
