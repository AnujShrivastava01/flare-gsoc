# Contributor Guidance
*FLARE @ Google Summer of Code 2026*

This document explains what we expect from applicants to Mandiant FLARE projects in GSoC 2026. While we've provided links and an application template, we probably haven't anticipated every question. So, reach out and talk with us!

All of our project ideas revolve around reverse engineering tools. That is, we want to improve the lives of malware analysts through novel techniques and automation. To succeed in this domain, you should have a basic familiarity with reverse engineering or a strong desire to learn.

Our tools are used by thousands of analysts to identify, describe, and stop malware.


## Application Steps
0. **Read** the GSoC [timeline](https://developers.google.com/open-source/gsoc/timeline), [contributor responsibilities](https://developers.google.com/open-source/gsoc/help/responsibilities), and [FLARE project ideas](https://github.com/mandiant/flare-gsoc/blob/2026/doc/project-ideas.md).
  1. Before applying, **talk to your prospective mentors** and mention that you have an interest in their project by creating a new topic in [GitHub discussions](https://github.com/mandiant/flare-gsoc/discussions) and mentioning @mandiant/flare-gsoc. This way we can get to know each other and discuss project ideas.
  2. **Prepare a patch** related to the existing FLARE project to practice interacting with us on GitHub. **This should take you between one and four hours**. We have "good first issue" [tagged here](https://github.com/search?q=topic%3Agsoc-2026+org%3Amandiant+label%3A%22good+first+issue%22+state%3Aopen&type=Issues); you can claim and close one of these or find something else that interests you. You don't need to send more than one PR to fulfill this requirement - we just want to work out any kinks in our collaboration styles. We value bug fixes or improvements that show your familiarity with the code.
  * **IMPORTANT**
    * Please do *NOT* comment on an issue asking if you can work on it - just do it!
    * Please do *NOT* submit a PR just to check off a box, i.e., a meaningless or trivial fix.
    * See the *AI Tooling Guidance* section below!
  3. **Write your application** using the below template. **This should take you between two and six hours**.
  4. **Submit your application** to the Google system before the deadline. All applications must go through Google's application system; we can't accept any application unless it is submitted there.


# AI Tooling Guidance
While we advocate for the use of AI tools to streamline and improve your development process, such as for test generation, it remains essential to demonstrate your proficiency in the project's language and a solid grasp of the underlying codebase.

When using AI tools:
* Conduct a thorough review of all AI-generated code to ensure you fully validate and understand the logic.
* Be transparent about your usage by disclosing the specific tool(s) employed and providing the prompts you submitted.

For additional information, refer to the [GSoC's Guidance for Contributors using AI tooling in GSoC 2026 doc](https://docs.google.com/document/d/1t9GcIBnNXPNO6klRQvU8pL8-uV6afzLo6JUAM299suA/edit?usp=sharing).


# Application Template

## Descriptive Title of What You Want to do This Summer

### About Me

Name and GitHub Handle: <br/>
University / Program / Year / Graduation: <br/>
Contact Information: <br/>
Location / Time Zone: <br/>
Brief CV: (link or appendix)

### Background and Interests

Please answer the following questions.
  1. What is your background and which current interests do you have? (3-5 sentences)
  2. Do you have any background or experience in reverse engineering or malware analysis? If not, why are you interested in learning more about it? (5-8 sentences)
  3. As mentors and project coordinators, how can we best support  you on your open source journey? (3-5 sentences)


### Code Contribution

Link to a code contribution (usually a pull request) you have made to the FLARE organization.
  - This must represent your own work, although other developers may chime in to improve it.
  - You can link more than one if you want, but remember that quality is much more important than quantity.


### Project Information

#### Project Abstract
(1-3 paragraphs)

#### Detailed description
(1-3 pages, or as guided during discussion with potential mentor)

#### Weekly timeline
The default schedule for GSoC is 12 weeks, either full-time or part-time. See the GSoC timeline for precise dates and thoroughly review the [GSoC Time Management Guide](https://google.github.io/gsocguides/student/time-management-for-students). This template assumes you'll be using those 12 weeks; if you're doing an alternate schedule you can adjust appropriately.

Community Bonding: (List any prepwork you want to do before coding starts)

For each coding week below, list planned code deliverables. Break the project into weeks and estimate what you will have completed at the end of each one. This schedule can be adjusted later if needed.

  - *Week 1* - This should include some code, even if it's draft PRs that demonstrate you’re able to use our repos, CI/CD, tests, etc.
  - *Week 2*
  - *Week 3*
  - *Week 4*
  - *Week 5*
  - *Week 6* - Midterm point. You need enough done at this point for your mentor to evaluate your progress. They will determine if you pass and can continue. Usually you want to be a bit more than half done.
  - *Week 7*
  - *Week 8*
  - *Week 9*
  - *Week 10*
  - *Week 11* - You may want to try to "feature freeze" in week 11 and focus on code integration and documentation cleanup in week 11-12. Additionally, you can work on a blog post talking about your experience and achievements.
  - *Week 12*
  - *Final week* - This week you will be submitting your projects.
