# Application Review

#### Need: 
We need to review ~1.5K+ applications for GenAI Genesis hackathon
#### Goals: 
1. Review as fast as possible since there are many applicants
2. Get people to learn how to provide consistent results 

#### Requirements/Objectives/Evaluation Criteria:
1.1) **Time:** The committee shall review all applicants within a 2-3 week window, such that rolling applicants will be reviewed immediately. The faster they are reviewed, the better.

1.2) **Task Delegation:** The committee will be divided up and review applicants based on alphabetical order, in the *initial phase* (i.e. as applicants roll in through the 1-week window). Division for the *initial phase* will be conducted via:

```python 
alphabets_per_team = (int)(26 letters / (reviewers/2))

'''
Partners will then be assigned letters based on the split
i.e: if the formula evaluates to 13, this means there are 4 reviewers, so 2 pairs of reviewers. Therefore:
'''

reviews = dict()
reviews["pair1"] = {"A to M"}
reviews["pair2"] = {"N to Z"}
```

After the *initial phase*, we enter the *final phase* where the application window has closed and we review those who have not been reviewed yet during the application window. We then will split up based on how many people reviewers have already reviewed and delegate more applicants to reviewers who have reviewed less people to ensure fair split:

```python

number_of_applications_per_team = (int)(num_of_applicants / (reviewers/2))
remaining_applicants = number_of_applicants

def number_of_applicants_left_to_review(already_reviewed: int) {
	return max(0, number_of_applications_per_team - already_reviewed)				   
}

reviews = dict()
reviews["pair1"] =  number_of_applicants_left_to_review(already_reviewed_team1)

reviews["pair2"] = number_of_applicants_left_to_review(already_reviewed_team2)

for pair in reviews.keys():
	if reviews[pair] <= 0:
		remaining_applicants -= number_of_applications_per_team 
		reviews[pair] = 0 
		
# Assign remaining applicants to a pair that still needs to review more
for pair in reviews.keys(): 
	if remaining_applicants > 0: 
		reviews[pair] += min(remaining_applicants, number_of_applications_per_team) 
		remaining_applicants -= min(remaining_applicants, number_of_applications_per_team)

```

1.3) **Reviewing Process:** The committee shall review applicants in accordance to the provided rubric (although individual judgement is also important). Reviewers will give a score from 0-12(?). If an applicant scores above a certain threshold (threshold > 8? -- needs to be decided), then they pass and can participate in the hackathon.

2.1) **Consistency:** The committee shall be provided with a few example scoring case studies/scenarios (maybe from past years) to help familiarize themselves with *scoring through comparison*, which will help them learn how to score and differentiate applicants.
