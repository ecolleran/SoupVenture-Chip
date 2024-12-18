CSE 30342 - Digital Integrated Circuits - University of Notre Dame 
Final Project - “SoupVenture”

Emily Colleran - ecoller2@nd.edu
Maggie Dempsey - mdempse4@nd.edu
Daniel Harrison - dharri23@nd.edu
Mary Menger - mmenger@nd.edu


SoupVenture is a state machine project designed to provide personalized soup recommendations. By answering a series of questions about preferences such as diet, temperature, texture, and more, users receive four tailored soup suggestions from a curated list of 16 options.

Welcome to our Souperia! Let’s get soupy!

How it works:

Users are presented with a series of questions to define their soup preferences. These questions narrow down options, ensuring personalized soup recommendations. The categories include:

Dietary Restrictions: Users can specify if they are gluten-free, vegetarian, or have no dietary restrictions.
Soup Temperature: Users choose whether they prefer cold or hot soups.
Color Preference: Options include yellow, green, or red soups.
Texture Preference: Users specify whether they like chunky or smooth soups.
Country of Origin: Users indicate whether they are interested in soups from Mexico, France, Texas, or Italy.
Noodle Preference: Users specify whether they want soups with noodles or not.
Failsafe Bean Soup: A failsafe ensures a recommendation of black bean soup if there’s an issue or logical error.

Inputs (Significance of inputs):

Clock (clk) (Controls state transitions and starts at 0)
Reset (rst) (Resets the state machine and starts at 0)
[1:0]  diet (00: Gluten free 01: Veg 10: None) 
temp (0: Cold 1: Hot)
[1:0] color (00: Yellow 01: Green 10: Red)
texture (0: Chunky 1: Smooth [1:0])
country (00: Mexico 01: France 10: Texas 11: Italy)
noodle (0: No 1: Yes)

The internal register soupcounter keeps track of the number of recommendations assigned, ensuring the system generates exactly four soups.

Outputs

SoupVenture generates four soup recommendations as four 4-bit outputs: soup1, soup2, soup3, and soup4. Each soup has a unique 4-bit identifier corresponding to one of 16 possible soups.
The soups include Chicken Noodle Soup, Chili, Tomato Soup, Celery Soup, Broccoli Cheddar Soup, Taco Soup, Black Bean Soup, Lobster Bisque, Sausage Tortellini Soup, Ramen, Italian Wedding Soup, French Onion Soup, Butternut Squash Soup, Lentil Soup, Gazpacho, and Pea Soup. 

State Transitions
SoupVenture operates via a finite state machine (FSM) with nine states:
Start State: The system initializes soup recommendations and clears all registers. The soupcounter is set to zero, and the machine transitions to the diet_state.
Dietary Restrictions State (diet_state): This state eliminates soups that don’t fit dietary restrictions. Gluten-free users avoid soups like French Onion and Chicken Noodle, while vegetarian users avoid Lobster Bisque and Sausage Tortellini Soup. After filtering, the machine transitions to the temp_state unless the soupcounter reaches three, in which case it moves directly to the finish state.
Temperature State (temp_state): In this state, the system recommends soups based on the user’s temperature preference. For cold soups, options like Gazpacho and Pea Soup are suggested. Hot soup lovers are directed to the texture_state.
Color Preference State (color_state): Soups are filtered based on the user’s preferred color. For yellow soups, options such as Butternut Squash and Broccoli Cheddar are recommended. For green soups, choices like Celery Soup and Pea Soup are offered. After this state, the system transitions to the country_state unless three soups have already been recommended.
Texture State (texture_state): Chunky soups like Chili are recommended for users who select chunky textures. Smooth soup lovers receive options such as Tomato Soup.
Country of Origin State (country_state): Soups are recommended based on the user’s preferred region. Mexican soups include Taco Soup, French soups include French Onion Soup, Texan soups include Chili, and Italian soups include Italian Wedding Soup.
Noodle Preference State (noodle_state): For users who select soups with noodles, options like Chicken Noodle Soup, Ramen, and Sausage Tortellini Soup are prioritized. The system transitions to the bean_state unless three soups have been selected.
Failsafe State (bean_state): To ensure the process doesn’t fail, the system recommends soups such as Black Bean Soup or Chili as backups. This state helps avoid logical errors and ensures the soupcounter reaches four.
Finish State: Once four soups are assigned, the machine resets to the start state, allowing for a new round of soup recommendations.


