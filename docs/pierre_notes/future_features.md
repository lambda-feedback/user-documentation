# Features for the Future
## Web App
- Skeleton placeholder loading for all sets, as well as sets list, while content is being fetched from the api. 
- Moving from a React SPA to Next.js or Gatsby in order to utilise caching and server side rendering (should make it faster)
- Better MathJax rendering (custom npm package?)
	- Deal with the non-typset math flashing for a second on page load
- Reactions
- Comments
- Microsoft stream embedding
- **Analytics implementation (Google analytics?)**
- Deal with `input_symbols`

### Response Areas
- Live updating latex component (displays rendered latex as the user enters it)


## Overall Lambda Function
- Startup shell script which registers a new ECR and Lambda function based on a supplied name. 
	- (or most likely on AWS CloudFormation, or npm serverless) (Architecture as code!)


## Grading Functions 
## Algorithm Functions
- Implement a Mathpix algorithm layer
- Implement a global unit converter 

## Mad Ideas
- Student 'credits', can use them to get a personal response from a teacher about a question
- MechNet Implementation
- Students can upload their own solutions to be displayed
	- They can be checked and endorsed by tutor
	- Can be downloaded and viewed by other students (worked solns)

## Testing
- A *Chaos Monkey* type of testing for all grading functions, once structure scales, could be useful to make sure error handling works