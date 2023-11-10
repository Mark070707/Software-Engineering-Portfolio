# Software Engineering Week9 submission Project work 2

## The Task
In week 9, you are continuing with the team project. Your portfolio entry should 
demonstrate how your software engineering practice is improving. It should include
much the same content as last week's:

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

In the reflective sections, try to identify things that you have done better this week. 
This could include, for example,

* Better application of the principles of clean code.
* Avoiding the repetition of previous mistakes.
* More comprehensive test coverage.
* Adoption of a more systematic personal workflow.
* Improved identification of problems in other people's code.
* etc.

## The Issue number 63
As an UNDAC Deputy Team Leader I want to view the stock levels of existing resources so
that I can ensure sufficient supplies at all times.

## The code
The provided code is aimed at displaying stock levels using a ListView. The main focus is
initializing a list of resources and displaying their stock levels.
Overall, the code reflects good encapsulation, separation of concerns, and appropriate use
of data structures, falling naming conventions, indentation, spacing and no code smells.
This has aspects of solid software design. With these practices, the codebase is more maintainable
and scalable, making it easier to implement additional features or modify existing ones in the future.
```
using System.Collections.ObjectModel;
using UNDAC_App.Models;

namespace UNDAC_App
{
    public partial class ViewStockLevel : ContentPage
    {
        public ObservableCollection<ResourceItem> Resources { get; set; }

        public ViewStockLevel()
        { 

        InitializeComponent();
        InitializeResources();
        DisplayStockLevels();
        }

    private void InitializeResources()
    {
        Resources = new ObservableCollection<ResourceItem>
            {
                new ResourceItem { ResourceType = "Macbook pro", CurrentStock = 32 },
                new ResourceItem { ResourceType = "Iphone 15", CurrentStock = 44 },
                new ResourceItem { ResourceType = "Ipad pro", CurrentStock = 75 },
                //add more resources
            };
    }

    private void DisplayStockLevels()
    {
        try
            { 

                stockLevelListView.ItemsSource = Resources;
        }
        catch (Exception ex)
        {
                Console.WriteLine("An error occurred while displaying stock levels: " + ex.Message);
        }
    }
    }
}
```

## Code summary
I have paired up with another student to work on the issue and review each others code. This will
guarantee the code gets reviewed. My coded was reviewed with no errors or feedback given. I learned from
the last code review to add comments to only relevent code. The code is a very small so it did not take
long to review. The same with reviewing the other studnts work, it was small with no negitive feedback given.

2 tests was done on my code using xunit. I tested the function InitializeResources() and DisplayStockLevels().
The tests passed as expacted. My program is just a small part of the the teams program, i can see how large
projects would need many tests, possibly testing departments.

## Reflection
This week's coding challenge felt more manageable as I teamed up with a colleague. Having someone to review
my code brought me a sense of reassurance. While I'm still in the process of fully grasping the C# language,
I'm glad the coding involved wasn't overly complex. My growing familiarity with GitHub and its navigation
has been a positive progression each week. Earlier, our team faced an issue where only the repository creator
had access, but now, the problem is the opposite with members frequently pushing to the main branch and causing
errors. Fortunately, one of our team members caught a minor spelling mistake, which was promptly fixed and merged,
restoring stability, at least for now.

Studying good coding practices and learning about code smells has enhanced my ability to discern quality code
when reading and writing. In the past, understanding someone else's program was a challenge during my college days,
but now, in class, it's becoming easier, especially when the code adheres to basic principles. Recently, a classmate
shared their code with me, and I noticed similarities in our coding styles, indicating that we're all on the same
page. This alignment has improved the overall collaboration, now documenting feedback during code reviews
is a significant challenge due to there being nothing to pick them up on.
