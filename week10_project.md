# Software Engineering Week10 submission Project work 3

## The Task

Week 10 is the third and last week in a series in which the goal is to improve your 
personal software engineering practice. Your portfolio entry has the same general content
as last week's, including:

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

In the reflective sections this week, you should highlight ways that you persona practice
has improved as before. It would also be good to reflect on any improvements that have
been made to the agreed team workflow and related procedures. Are things working
better than they were? What further improvements could be made in the future?

## The Issue number 51
As an UNDAC Deputy Team Leader I want to view Security Alerts Page.

## The Code
```
using System.Collections.ObjectModel;
using UNDAC_App.Classes;
using UNDAC_App.Models;

namespace UNDAC_App.Views;

public partial class SubTeamStatusView : ContentPage
{

	private ObservableCollection<SubTeamStatus> SubTeamStatusList;
	private SubTeamStatusManager subTeamStatusManager;

	public SubTeamStatusView()
	{
		InitializeComponent();

		subTeamStatusManager = new SubTeamStatusManager();
		SubTeamStatusList = new ObservableCollection<SubTeamStatus>(subTeamStatusManager.GetAllSubTeamStatus());

		SubTeamStatusListView.ItemsSource = SubTeamStatusList;
	}

	private async void OnAddSubTeamStatusClicked(object sender, EventArgs e)
	{
		var newStatus = new SubTeamStatus();
		newStatus.subTeamName = await DisplayPromptAsync("New Sub Team Status", "Please enter the Sub Team's name");
        newStatus.status = await DisplayPromptAsync("New Sub Team Status", "Please enter the Sub Team's status");
        newStatus.issue = await DisplayPromptAsync("New Sub Team Status", "Please describe the issue");
        newStatus.resolution = await DisplayPromptAsync("New Sub Team Status", "Please describe your resolution");

		if (!string.IsNullOrWhiteSpace(newStatus.subTeamName) && !string.IsNullOrWhiteSpace(newStatus.status) &&
			!string.IsNullOrWhiteSpace(newStatus.issue) && !string.IsNullOrWhiteSpace(newStatus.resolution))
		{
			subTeamStatusManager.AddSubTeamStatus(newStatus);
			SubTeamStatusList.Add(newStatus);
		}
    }

	private async void OnSubTeamUpdateClicked(object sender, EventArgs e)
	{
		var button = sender as Button;
		var statusToModify = button?.CommandParameter as SubTeamStatus;

		if (statusToModify != null)
		{
			var newSubTeamName = await DisplayPromptAsync("Update Sub Team Status", "Please enter the new Sub Team name", initialValue: statusToModify.subTeamName);
            var newStatus = await DisplayPromptAsync("Update Sub Team Status", "Please enter the new Sub Team status", initialValue: statusToModify.status);
            var newIssue = await DisplayPromptAsync("Update Sub Team Status", "Please enter the new Sub Team issue", initialValue: statusToModify.issue);
            var newResolution = await DisplayPromptAsync("Update Sub Team Status", "Please enter the new Sub Team resolution", initialValue: statusToModify.resolution);

            if (!string.IsNullOrWhiteSpace(newSubTeamName) && !string.IsNullOrWhiteSpace(newStatus) &&
            !string.IsNullOrWhiteSpace(newIssue) && !string.IsNullOrWhiteSpace(newResolution))
            {
                statusToModify.subTeamName = newSubTeamName;
				statusToModify.status = newStatus;
                statusToModify.issue = newIssue;
                statusToModify.resolution = newResolution;
				
				subTeamStatusManager.UpdateSubTeamStatus(statusToModify);

				SubTeamStatusList.Clear();

				foreach(var subTeam in subTeamStatusManager.GetAllSubTeamStatus())
					SubTeamStatusList.Add(subTeam);
				
			}
        }        
    }

	private void OnSubTeamDeleteClicked(object sender, EventArgs e)
	{
		var button = sender as Button;
		var statusToDelete = button?.CommandParameter as SubTeamStatus;

		if (statusToDelete != null)
		{
			subTeamStatusManager.DeleteSubTeamStatus(statusToDelete.Id);
			SubTeamStatusList.Remove(statusToDelete);
		}
	}

}
```

## Code Snippets and Design Practices
ObservableCollection Usage:

```
private ObservableCollection<SubTeamStatus> SubTeamStatusList;
```
This shows adherence to good software design practices by using ObservableCollection.
It enables the UI to automatically update when items are added, changed, or removed,
improving user experience and software responsiveness.

## Initialization in Constructor:

```csharp
public SubTeamStatusView()
{
    InitializeComponent();
    subTeamStatusManager = new SubTeamStatusManager();
    SubTeamStatusList = new ObservableCollection<SubTeamStatus>(subTeamStatusManager.GetAllSubTeamStatus());
    SubTeamStatusListView.ItemsSource = SubTeamStatusList;
}
```
Initializing the SubTeamStatusManager and SubTeamStatusList in the constructor ensures that
the view is properly set up with the necessary data upon instantiation.

## CRUD Operations:

Addition, modification, and deletion methods (OnAddSubTeamStatusClicked, OnSubTeamUpdateClicked, OnSubTeamDeleteClicked)
are clear and concise, indicating good practice in organizing code for maintainability and readability.

## Testing
Comprehensive tests were written to cover all functionalities introduced in this feature, including:

Adding new sub-team statuses.<br>
Updating existing statuses.<br>
Deleting statuses.

## Code Review
I recieved positive feedback on my code review by following the basic principles and naming conventions. I also
gave positive feedback to my team partner, however i did give some sugestion that it would be great to
have a intro comments at the start of the code to explain what it does. I explained that the code it great
and clear but it would prevent the a developer having to read all the code to understand what it does but
having a quick explanation would save time.

## Reflection
Personal Improvements with code reviewing and navgation with GitHub have been great. I am starting to
enjoy the use of gitHub. I have realized the importance of consistent naming conventions for better readability
that reduces the need for comments. I have learned to write more efficient tests covering edge cases, however
i have been trying mock testing unsuccessfully, I will spend more time researching this to get it up and
running by the final report.Team Workflow and Procedure Improvements have been made by the team in the speed
of which issues are being completed and reveied, particularly in the code review process, with more active participation
and constructive feedback for most people.Compared to peers, my approach to error handling and testing has been lacking, i look to improve this overtime.
Common problems in team situations often relate to miscommunication, which we've started
to address by having more frequent updates by asking how everyone is getting on, this usually starts a
converstaion by only some people, but this is an improvement.

