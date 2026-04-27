---
# Do not edit the text between these lines!
layout: default
---

# This is a big header

<!-- This is a comment. Below, you'll see code for inserting an image. To make this image appear, update <custom-path>. To add an image, save it inside the imgs folder of this repository. -->
<img src="<custom-path>/static/imgs/logo.png" alt="Image of Comp110 rainbow logo. "  width="500"/>

## This is a small header

This is basic paragraph text.

THIS IS A TEST

## Part 1: Analysis for Continuous Improvement

Continuous Improvement embraces a belief there is _always room to make things better_. It is a mindset and process we value and practice in this course. In this assignment, you are able to practice continuous improvement and contribute to the design ideas of the course.

### Brainstorming Ideas

Reflect on your personal experiences and observations in COMP110 and **brainstorm modifications to the course that _create value_ beyond its current design**. When brainstorming, try not to be critical of the ideas you come up with regarding scale, stakeholders impacted, or for any other reasons. In the markdown cell below, brainstorm 3 to 5 ideas you think would create value for you.

Each brainstormed idea should state a. the suggested change or addition, b. what the expected value created, and c. which specific stakeholders would benefit.  If helpful, expand on the following template "The course should (state idea here) because it will (state value created here) for (insert stakeholders here)."

Example A: "The course should use only examples from psychology experiments because it will be more relevant for students who are psychology majors."

Example B: "The course should not have post-lesson questions because they are not useful for most students in the class."

### Part 1.1: Creative Ideation

1. The course should invite guest speakers from different industries who utilize python within their companies/professional roles to demonstrate the usefullness of the course outside of the computer science commuity (ex: biomedical companies, environmental science research orgs).  This would enhance the course instructors connections beyond Carolina and benefit student connections and career paths as well.
2. The course should give practice examples before quizzes that are aimed at "debugging" code.  These could include examples of key functions/practices learned in that unit so that students know the exact syntax of the code and how to implement it properly.
3. The course should include a brief showcase of other COMP classes to take at UNC after completing COMP110 for students who are interested in pursuing a computer science major or minor.
4. The course should make one assignment where students are able to choose a data set of their own to analyze so that they are better able to express their own research interests.  This would help implement how python and computer science are applicable to many fields of work!
5. The course should publish a "common mistakes" section of the pre-quiz study guides to allow students in the course to learn from peer mistakes, and tighten key utility/code usage without making the same errors.

### Part 1.2: Identifying Missing Data

1. Idea without sufficient data to analyze: The idea of the debugging section of the quiz study guide would have insufficient data to determine whether or not it would be worth implementing.

2. Suggestion for how to collect data to support this idea in the future: In order to collect data on "debugging" code section usefullness in the future, a randomly selected group of students could receive a run through and practice examples of debugging before taking the quiz while another randomly selected group of students take the quiz without this practice.  After the quiz, a poll would be distributed asking the students whether or not they felt prepared for the quiz (ex: Debugging practice activities helped me feel more prepared and confident about course topics going into the quiz 1 strongly disagree-7 strongly agree).  The answers from this poll partnered with student scores on the quiz from each of the two randomly selected groups could then be cross compared to determine the usefullness of implementing this section on the pre-quiz study guide.

#### Choosing an Idea to Analyze

Consider those of your ideas which _do_ seem likely to have relevant data to analyze. If none of your ideas do, spend a few minutes and brainstorm another idea or two with the added connection of data available on hand and add those ideas to your brainstormed ideas list.

Select the one idea which you believe is _most valuable_ to analyze relative to the others and has data to support the analysis of. In the markdown cell for Part 3 below, identify the idea you are exploring and articulate why you believe it is most valuable (e.g. widest impact, biggest opportunity for improvement, simplest change for significant improvement, and so on).

### Part 1.3: Choosing Your Analysis

1. Idea to analyze with available data: I believe that idea #3 regarding a showcase of courses offered in computer science to pursue after COMP110 for those interested in pursuing a COMP minor or major is the most valuable because it addresses a high-impact decision point for students taking the COMP110 course.  COMP110 often serves as the first course into the computer science major or minor, yet many students may lack visibility into what lies next in their curriculum.  By improving transparency around course pathways, this initiative has the potential to support student retention in the COMP major or minor, reduce uncertainty about the computer science pathway, and provide extra support around informed academic planning.  In order to analyze this idea, I will look at declared majors/minors, other COMP courses completed, and prior time spent coding on own time.

2. This idea is more valuable than the others brainstormed because: showcasing other COMP courses would enhance the COMP community, and further demonstrate unwavering support of both staff and peer students who have progressed further through the computer science major.  Additionally, this idea impacts more individuals than just those who are struggling in the COMP110 course, whereas ideas 2 and 5 are aimed more directly at those looking for more practice and assistance with code taught in the course.  Furthermore, this idea could connect directly to measurable outcomes, such as increasing the number of individuals enrolled in the COMP110 course, rates of COMP major/minor declaration, and improved retention in the computer science pipeline (measured unerollment rates/major switches).

#### Your Analysis

Before you begin analysis, a reminder that we do not expect the data to support everyone's ideas and you can complete this exercise for full credit even if the data does not clearly support your suggestion or even completely refutes it. What we are looking for is a logical attempt to explore the data using the techniques you have learned up until now in a way that _either_ supports, refutes, or does not have a clear result and then to reflect on your findings after the analysis.

Using the utility functions you created for the previous exercise, you will continue with your analysis in the following part. Before you begin, refer to the rubric on the technical expectations of this section in the exercise write-up.

In this section, you are expected to interleave code and markdown cells such that for each step of your analysis you are starting with an English description of what you are planning to do next in a markdown cell, followed by a Python cell that performs that step of the analysis.

Additionally, you will be producing charts or visualizations as part of your analysis via the Python package `seaborn`. Refer to the previous section on python packages and data visualization for more information on how to use this package and to the rubric for what will be required.

to best guage the interests of the majority of the class to determine if sharing more about future courses will be worthwhile.

# I will start the data analyzation by importing the code 
from data_utils import read_csv_rows, head, columnar, select, count

data_rows = read_csv_rows("data/survey_izzi.csv")
data_cols = columnar(data_rows)
head(data_cols, 5)

## Narrowing down the data set to only include rows/columns useful for this analysis

I want to look at students majors, other COMP classes they have taken, and how much time they spend coding outside the scope of this course.  In order to do so, I will need the columns 'major', 'other_comp', and 'prior_time'.  I will use the select function below to create a new table with just these columns and print out the first couple of values to ensure proper function.

relevant_data = select(data_cols, ["major", "other_comp", "prior_time","comp_major"])
head(relevant_data, 10)

In order to help determine whether or not students are interested in computer science, I want to see if there is a correlation between taking COMP110 and having prior COMP experience at UNC.  I will represent this through a scatter plot to best depict the relationship of taking different courses and further pursuing COMP110.

import matplotlib.pyplot as plot

sns.relplot(
    data=relevant_data,
    kind="scatter",
    x="comp_major",
    y="other_comp",
    hue="comp_major"
)
plot.xticks(rotation=30, ha="right")
plot.title("COMP Major Status vs. Prior COMP Course Experience")
plot.tight_layout()
plot.show()

img src="<static\priorexperience.png" alt="COMP Major Status vs. Prior COMP experience Graph. "  width="500"/>


To understand whether or not a showcase of other COMP courses would reach meaningful audience, I want to see how many people in the class are COMP majors.  To do so, I will use count on the 'majors' column in relevant_data.

major_counts = count(relevant_data["major"])
print(major_counts)

# a plot to demonstrate the amount of each declared major
import seaborn as sns
import matplotlib.pyplot as plot
sns.set_theme()

sns.catplot(
    data=relevant_data,
    kind="count",
    x="major"
)
plot.xticks(rotation=45, ha="right")
plot.title("Declared Majors in COMP110")
plot.tight_layout()
plot.show()


img src="<static\declaredmajor.png" alt="COMP 110 Student Majors."  width="500"/>

Additionally, I want to see how many students intend to delcare a COMP major or minor.  To do so I will call count on comp_major.

comp_major_counts = count(relevant_data["comp_major"])
print(comp_major_counts)

# Distribution plot of COMP majors and minors in COMP110

sns.catplot(
    data=relevant_data,
    kind="count",
    x="comp_major"
)
plot.xticks(rotation=30, ha="right")
plot.title("Are COMP110 Students Pursuing a COMP Major or Minor?")
plot.tight_layout()
plot.show()

img src="<static\majorminor.png" alt="COMP Major or Minor Interest."  width="500"/>

Now, I want to see what proportion of students in the class are pursuing a COMP major or minor, to see if this presentation of other COMP courses would be suitable for the majority of the class, or best expressed through an email or external link that students could interact with if interested.  To do so, I will define a new function called filter_columns.  filter_columns will:
- take in an input table, a column name, and a target value (in this case the desired major)
- return a new table with only rows where the column matched the desired target value


from data_utils import filter_column

Now, I will use filter column to separate out the number of students who answered Computer Science to their current declared major.

I will also use this filter to separate out the number of students who answered Yes - BA, Yes - BS, and Yes - Minor to comp_major (their intention to pursue comp science).

comp_majors = filter_column(relevant_data, "major", "Computer Science")
print(len(comp_majors))

BA_yes = len(filter_column(relevant_data, "comp_major", "Yes - BA"))
BS_yes = len(filter_column(relevant_data, "comp_major", "Yes - BS"))
minor_yes = len(filter_column(relevant_data, "comp_major", "Yes - Minor"))

interested_in_comp_count = BA_yes + BS_yes + minor_yes
print(interested_in_comp_count)


Since I have found the number of current Computer Science majors, and the number of people interested in pursuing the major or minor I will now find the total percentage of people in the class "interested" in computer science by sheer metric of individuals in the major or desiring to pursue computer science studies at UNC.  In doing so, I am determining whether or not the description of other COMP courses at UNC is speaking to the masses!  If at least 50% of the students in COMP110 currently "are interested" then this will tell us to showcase these future classes, if less than 50% "are interested" this will tell us to send an email or link to these classes.

comp110_students = len(relevant_data["major"])

percent_interested = (interested_in_comp_count/comp110_students) * 100

if percent_interested < 50:
    print (f"Only {percent_interested} percent students are interested in computer science.  It would be best to send this information as a link and spend more class time on review or addressing student questions!")

else:
    print (f"{percent_interested} percent students are interested in computer science, describe the scope of the major in class and suggest a couple of courses to follow COMP110 with!")

#### Conclusion

In the following markdown cell, write a reflective conclusion given the analysis you performed and identify recommendations.

If your analysis of the data supports your idea, state your recommendation for the change and summarize the data analysixs results you found which support it. Additionally, describe any extensions or refinements to this idea which might be explored further. Finally, discuss the potential costs, trade-offs, or stakeholders who may be negatively impacted by this proposed change.

If your analysis of the data is inconclusive, summarize why your data analysis results were inconclusive in the support of your idea. Additionally, describe what experimental idea implementation or additional data collection might help build more confidence in assessing your idea. Finally, discuss the potential costs, trade-offs, or stakeholders who may be negatively impacted by experimenting with your idea.

Finally, if your analysis of the data does not support it, summarize your data analysis results and why it refutes your idea. Discuss the potential costs, trade-offs, or stakeholders who may be negatively impacted by this proposed change. If you disagree with the validity of the findings, describe why your idea still makes sense to implement and what alternative data would better support it. If you agree with the validity of the data analysis, describe what alternate ideas or extensions you would explore instead. 


### Part 1.5: Conclusion

In conclusion, further analysis of primary majors, intended pursuit of computer science, and prior coding experiences demonstrates that showcasing COMP courses at UNC to pursue post-COMP110 completion is not worthwhile.  Only 2.247191011235955 percent of students are "interested" in computer science meaning they have either declared the major or minor, or are interested in doing so, meaning the majority of the class is already pursuing or is interested in pursuing other fields of study.  With this in mind, I believe it would still be worthwhile to send out an email or link with course information to the class to demonstrate to the students interested that although they are in the minority amongst their peers, that the staff and peers further accelerated throughout the program are encouraging, supportive, and knowledgable on the field.  Potential trade-offs of not discussing this information in person is lack of access to students interested in pursuing computer science who may not have access to the technology or internet needed in order to receive messages outside of class.  Additionally, stakeholders (being the COMP professors and undergraduate TAs) would need to use more time and resources (website and extra communication platforms specific to only the students who are interested) in order to execute this communication.  Rather, it may be a good idea to still implement this idea by taking a quick poll and raise of hands and announce that the professor and undergraduate TAs are avaiable for a brief period of time to discuss courses after class, or in regularly scheduled office hours!
