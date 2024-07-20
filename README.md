# sabias-que
aplicacion ios
#import <UIKit/UIKit.h>

@interface ViewController : UIViewController

@property (weak, nonatomic) IBOutlet UISegmentedControl *segmentedControl;
@property (weak, nonatomic) IBOutlet UIButton *showFactButton;
@property (weak, nonatomic) IBOutlet UILabel *factLabel;

- (IBAction)showFactButtonTapped:(id)sender;

@end
#import "ViewController.h"

@interface ViewController ()

@property (strong, nonatomic) NSArray *factsScience;
@property (strong, nonatomic) NSArray *factsHistory;
@property (strong, nonatomic) NSArray *factsTechnology;
@property (assign, nonatomic) NSInteger currentFactIndex;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Initialize facts arrays
    self.factsScience = @[@"Fact 1 about Science.",
                          @"Fact 2 about Science.",
                          @"Fact 3 about Science."];
    
    self.factsHistory = @[@"Fact 1 about History.",
                          @"Fact 2 about History.",
                          @"Fact 3 about History."];
    
    self.factsTechnology = @[@"Fact 1 about Technology.",
                             @"Fact 2 about Technology.",
                             @"Fact 3 about Technology."];
    
    self.currentFactIndex = -1; // Start with index -1 to show the first fact on first tap
}

- (IBAction)showFactButtonTapped:(id)sender {
    // Determine which category is selected
    NSInteger selectedIndex = self.segmentedControl.selectedSegmentIndex;
    
    // Determine which facts array to use based on selected category
    NSArray *factsArray;
    switch (selectedIndex) {
        case 0:
            factsArray = self.factsScience;
            break;
        case 1:
            factsArray = self.factsHistory;
            break;
        case 2:
            factsArray = self.factsTechnology;
            break;
        default:
            factsArray = @[]; // Default to empty array if unexpected index
            break;
    }
    
    // Update the fact label with the next fact
    self.currentFactIndex++;
    if (self.currentFactIndex >= factsArray.count) {
        self.currentFactIndex = 0; // Wrap around if reached end of array
    }
    self.factLabel.text = factsArray[self.currentFactIndex];
}

@end
