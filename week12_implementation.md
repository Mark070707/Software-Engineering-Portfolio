# Software Engineering Week12 submission Project work 5

## The Task

Week 12 aims to integrate everything covered in the module.

Your portfolio entry should demonstrate your abilities, highlight improvements that you
have made during the course of the module and show your capacity to learn from experience
through clear analytical reflection. The structure of this entry is similar to those from 
weeks 8-10:

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

As with the earlier entries related to the team project, the reflective sections should
consider your own practice and team processes. In addition, this is a good point to
include your thoughts on the general challenges related to working in a software
development team and the most effective methods to streamline operations and to safeguard
the quality of the end product.

## The Issue number 84

## The code
```csharp
/*
   DisasterManagementPage - Manages disaster management needs.

   This program allows users to view, add, modify, and delete disaster management needs.
*/

using System;
using System.Collections.ObjectModel;
using Microsoft.Maui.Controls;
using UNDAC_App.Classes;
using UNDAC_App.Models;

namespace UNDAC_App
{
    public partial class DisasterManagementPage : ContentPage
    {
        private ObservableCollection<DisasterManagementNeeds> disasterManagementNeedsList;
        private DisasterManagementNeedsManager disasterManagementNeedsManager;

        // Constructor
        public DisasterManagementPage()
        {
            InitializeComponent();

            disasterManagementNeedsManager = new DisasterManagementNeedsManager();
            disasterManagementNeedsList = new ObservableCollection<DisasterManagementNeeds>(disasterManagementNeedsManager.GetAllDisasterManagementNeeds());

            DisasterManagementNeedsListView.ItemsSource = disasterManagementNeedsList;
        }

        // Event handler for adding a new disaster management need
        private async void OnAddDisasterManagementNeedClicked(object sender, EventArgs e)
        {
            var newNeed = new DisasterManagementNeeds();
            newNeed.NeedName = await DisplayPromptAsync("New Need", "Enter the need name:");
            newNeed.Urgency = await DisplayPromptAsync("New Need", "Enter the urgency:");
            newNeed.Location = await DisplayPromptAsync("New Need", "Enter the location:");
            newNeed.Description = await DisplayPromptAsync("New Need", "Enter the description:");
            var requiredQuantityInput = await DisplayPromptAsync("New Need", "Enter required quantity:");
            int.TryParse(requiredQuantityInput, out int requiredQuantity);
            newNeed.RequiredQuantity = requiredQuantity;

            if (!string.IsNullOrWhiteSpace(newNeed.NeedName) &&
                !string.IsNullOrWhiteSpace(newNeed.Urgency) &&
                !string.IsNullOrWhiteSpace(newNeed.Location) &&
                !string.IsNullOrWhiteSpace(newNeed.Description))
            {
                disasterManagementNeedsManager.AddDisasterManagementNeed(newNeed);
                disasterManagementNeedsList.Add(newNeed);
            }
        }

        // Event handler for modifying an existing disaster management need
        private async void OnDisasterManagementNeedsModify(object sender, EventArgs e)
        {
            var button = sender as Button;
            var selectedNeed = button?.CommandParameter as DisasterManagementNeeds;

            if (selectedNeed != null)
            {
                var updatedName = await DisplayPromptAsync("Modify Need", "Enter the new need name:", initialValue: selectedNeed.NeedName);
                var updatedUrgency = await DisplayPromptAsync("Modify Need", "Enter the new urgency:", initialValue: selectedNeed.Urgency);
                var updatedLocation = await DisplayPromptAsync("Modify Need", "Enter the new location:", initialValue: selectedNeed.Location);
                var updatedDescription = await DisplayPromptAsync("Modify Need", "Enter the new description:", initialValue: selectedNeed.Description);
                var requiredQuantityInput = await DisplayPromptAsync("Modify Need", "Enter the new required quantity:", initialValue: selectedNeed.RequiredQuantity.ToString());
                int.TryParse(requiredQuantityInput, out int updatedRequiredQuantity);

                if (!string.IsNullOrWhiteSpace(updatedName) &&
                    !string.IsNullOrWhiteSpace(updatedUrgency) &&
                    !string.IsNullOrWhiteSpace(updatedLocation) &&
                    !string.IsNullOrWhiteSpace(updatedDescription))
                {
                    selectedNeed.NeedName = updatedName;
                    selectedNeed.Urgency = updatedUrgency;
                    selectedNeed.Location = updatedLocation;
                    selectedNeed.Description = updatedDescription;
                    selectedNeed.RequiredQuantity = updatedRequiredQuantity;

                    disasterManagementNeedsManager.UpdateDisasterManagementNeed(selectedNeed);
                }
            }
        }

        // Event handler for deleting an existing disaster management need
        private void OnDisasterManagementNeedsDelete(object sender, EventArgs e)
        {
            var button = sender as Button;
            var selectedNeed = button?.CommandParameter as DisasterManagementNeeds;

            if (selectedNeed != null)
            {
                disasterManagementNeedsManager.DeleteDisasterManagementNeed(selectedNeed.Id);
                disasterManagementNeedsList.Remove(selectedNeed);
            }
        }

        // Event handler for handling tapped event for a disaster management need
        private void OnDisasterManagementNeedsTapped(object sender, ItemTappedEventArgs e)
        {
            // Handle tapped event for a disaster management need
        }
    }
}
```
## Testing
In the provided code, several methods have been tested in xunit to ensure their functionality.
Here's a breakdown of the methods that was tested.

Constructor (ViewSecurityAlertsPage()):
Tested that the SecurityAlerts collection is initialized.
Tested that the SecurityAlertDB instance is created.
Tested that the initial state of SecurityAlertsListview.ItemsSource is set correctly.

RefreshSecurityAlertsList() Method:
Tested that the method clears the SecurityAlerts collection.
Tested that it correctly adds new SecurityAlert objects to the collection.
Tested that it correctly reflects changes from the database.

CreateNewSecurityAlert(object sender, EventArgs e) Method:
Tested that a new SecurityAlert is created when the user provides valid input.
Tested that the method handles empty or null input appropriately.
Tested that the UI is correctly refreshed after creating a new alert.

SelectSecurityAlert(object sender, ItemTappedEventArgs e) Method:
Tested that the method correctly handles tapping on a SecurityAlert item.
Tested that the UI is updated after editing a selected alert.
Tested that the method handles null or invalid input.

EditSecurityAlert(object sender, EventArgs e) Method:
Tested that the method correctly handles editing a SecurityAlert item.
Tested that the UI is updated after editing an alert.
Tested that the method handles null or invalid input.

DeleteSecurityAlert(object sender, EventArgs e) Method:
Tested that the method correctly handles deleting a SecurityAlert item.
Tested that the UI is updated after deleting an alert.
Tested that the method handles null or invalid input.

## Code Review
I did 2 code reviews this week which is 1 more than usual. I know im not perfect at revieing other
peoples code yet but definatle improving. I did not see any code smells and only code good coding practices.

My code was revied, my feedback was that there is too many unnessassary comments to explain my code.
I dissagreed with the feedback, i felt that there just to much going on in the code and it needs short
explanations to help an other developer understand what is going on with ease. 

## Reflection
Over the past weeks, my journey in contributing to our team project on GitHub has been
marked by notable progress in both personal and team aspects, this has been a slow
learning curve to start with but feel it has been getting better. I also learned from speaking to my peers that by
inserting "csharp" at the start of my code snippet will add colour to my code in the repository.

Personal Growth:
In terms of code reviewing and GitHub navigation, I've experienced significant improvements.
The platform is becoming more enjoyable as I delve deeper into its functionalities.
One key realization has been the importance of adhering to coding principles. If i look back at
code i was producing before this modual it was very different, i have always felt i have had to
explain my code, but now it is alot clearer and the need for comments has reduced.

While I've become adept at crafting more efficient tests, the realm of mock testing has presented
a challenge. Acknowledging this, I am committed to dedicating more time to research and implementation,
aiming to have it seamlessly integrated into our project by the final report.

Team Workflow and Procedure Enhancements:
Collaboratively, our team has made commendable strides in the efficiency of issue resolution and code
review processes. Notably, there has been an uptick in active participation, with constructive feedback
becoming more commonplace. The team message comunication has ben more responsive in the spen of replys which
is great for team repport. This collective effort has contributed to a quicker turnaround in completing
tasks. I have found myself being able to complete more issues in and reviews in the same period of time.

Recognizing the need for improvement, I've identified disparities in my approach to error handling
and testing compared to my peers. This awareness serves as a catalyst for continuous improvement
in these areas.

In addressing common team challenges, we've initiated efforts to mitigate miscommunication.
Regular updates, where everyone shares their progress and challenges, have become a valuable practice.
Although participation in these conversations is not uniform, the mere initiation of such discussions
signifies an improvement in team communication.As I reflect on these aspects of my journey, the commitment
to continual learning and enhancement remains at the forefront. I look forward to further refining my
skills and contributing meaningfully to our collaborative efforts.