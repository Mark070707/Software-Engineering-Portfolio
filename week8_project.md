# Project work 1

In week 8, you are exercising all the principles and techniques that have been discussed 
in the module so far. Your portfolio entry should demonstrate your ability to integrate 
the various dimensions of software engineering into your practice. It should include 

* A descriptive summary of the issue that you worked on.
* Snippets from your code with commentary showing how you have used good software design 
  practice.
* A descriptive summary of the test code that you have written.
* A reflective summary of any changes that were requested during the code review along 
  with your fixes.
* A descriptive summary of any issues you found with the code that you were asked to review.
* A general reflective section that identifies, for example,
  * New things you have realised this week
  * Common problems that can arise in a team development situation
  * How your practice compares to other people's
  * etc.

Be sure to include links to the original items in the team's GitHub repository.

## The Issue number 67
As an UNDAC Deputy Team Leader I want to view a list of all local media agencies
so that I can contact them immediately.

## The code
This code creates a new page when a button is clicked and displayed a list od Media Agencies.
Overall, the code reflects good encapsulation, separation of concerns, and appropriate use of data structures,
falling naming conventions, indentation, spacing and no code smells. This has aspects of solid software design.
With these practices, the codebase is more maintainable and scalable, making it easier to implement additional
features or modify existing ones in the future.
```
using System.Collections.ObjectModel;

namespace UNDAC_App
{
    public partial class MediaAgencyList : ContentPage
    {
        // ObservableCollection for handling dynamic data changes and notifying the UI
        public ObservableCollection<Agency> Agencies { get; set; }

        public MediaAgencyList()
        {
            InitializeComponent();

            // Initialize the ObservableCollection with Agency objects
            Agencies = new ObservableCollection<Agency>
            {
                new Agency { Name = "The Sun" },  // Adding an instance of Agency with name "The Sun"
                new Agency { Name = "The Daily News" },  // Adding an instance of Agency with name "The Daily News"
                new Agency { Name = "The News Of The World" }  // Adding an instance of Agency with name "The News Of The World"
                // Additional Agency objects can be added here
            };

            // Set the ObservableCollection as the ItemsSource for the mediaAgencyListView
            mediaAgencyListView.ItemsSource = Agencies;
        }
    }

    // Simple class representing an agency
    public class Agency
    {
        public string Name { get; set; }  // Property to hold the name of the agency
    }
}

```
## Code summary
My coded was reviewed with no errors or feedback given apart form suggesting to give more comments
to provide better description of the code. I have taken on this feedback and added relevent comments.
I understand the importance for future to help any developer read an intoduction to the code and what
it does. I revieved a team members code,the code was very similar and also suggested adding comments
to code that is not self explanatory.A test was done on my code using xunit. The test passed as expacted.


## Reflection
I have found that the more i use GitHub the more comfortable i am navagating the site. I understand the
how important it is to use for a large company with many developers working as a team on the same project.

I the large team of 16 members with no distinct manager dificult to comunicate with, there seems to be sub
teams splitting and working together. I feel smaller teams of perhaps 5 would work better in this enviroment.
Due to the disconnect on comunication with all my team members, im not exactly sure who is in my team, i think
5 people comunicate on the team discord who all work different schedules and all work at different paces.
I think there is no bad experience as i can learn from these experiences to what works well and what does not
work well. I cant compare my practices to others yes but over the next few weeks of working on this team project
i hope to spend more time with them. Overall i am very very happy i actually comlpeted a team issue fully. 

