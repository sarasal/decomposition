This folder contains the SpiderDec, the decomposed version of the Spider dev data set as the dev-decomposed.json. 

It contains the following files:

- dev-decomposed.json
	# Training Examples: 1034
	# Databases:		 20
- README.txt



For each example in the Spider dev set, we assign a JSON object including database_id, interaction, and final.
Within the interaction list, sub-questions are saved. The Final object is the question we apply decomposition on.
Here an example is shown. 
Note that we name the execution result of each question as a table, tb1 is the execution result of sub-question 1, tb2 is the execution result of sub-question 2, and so on.

{
        "database_id": "tvshow",
        "interaction": [
            {
                "utterance": "what are the tv channels playing any cartoons directed by Ben Jones?",
                "query": "SELECT channel FROM cartoon WHERE directed_by = 'Ben Jones'"
            },
            {
                "utterance": "What are the package options of all tv channels that are not in tb1?",
                "query": "SELECT package_option FROM TV_Channel WHERE id EXCEPT (SELECT channel FROM cartoon)"
            }
        ],
        "final": {
            "query": "SELECT package_option FROM TV_Channel WHERE id NOT IN (SELECT channel FROM cartoon WHERE directed_by = 'Ben Jones')",
            "utterance": "What are the package options of all tv channels that are not playing any cartoons directed by Ben Jones?"
        }
}
