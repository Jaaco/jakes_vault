#ui #design #layout #book #resources
# Systemize Everything
systemizing everything reduces decision fatique down the line. limiting the amount of choices there are for a decision can speed up the development process and help keep everything standardized
examples:
- font size
- font weight
- line height
- color
- margin
- padding
- width
- height
- box shadows
- border radius
- opacity

## Font Weight System
usually 2 font weights are enough for an application:
normal (400 or 500) for most text
heavier (600 or 700) for emphasizing

fonts under 400 can be hard to read, especially for smaller sizes (some exceptions for large headings)

## Font Color System 
Usually 3 choices for font colors should be enough:
dark for primary content
gray for secondary content
lighter gray for tertiary content

**don't** use gray font on colored backgrounds since the desired effect is different to white background
**don't** use white text with less opacity for colored backgrounds since it could expose patterns or images from underneath
**do** pick a new color with the same hue but different saturation and lightness as the background color

# Personality in Design
## Color
#colors

## Fonts
### Sans Serif
- modern
- playful (rounded versions)
### Serif
- classic
- serious

## Border Radius
### Big Border Radius
- more playful
- modern
### Little Border Radius
- more serious


# Hierarchy
## Fonts
try not do implement hierarchy only with different font sizes
also use
- font weight
- font color

## Emphasize by De-Emphasizing
if you cannot emphasize an object (already emphasized), then de-emphasizing the related oblects can have the same effect.
eg.
- if multple items can be chosen, change the font color of the unselected ones
- remove the background of a navigation area that competes with main content

## Labels
### Avoid Labels
labels often add unnecessary information, that could be infered from the content
eg phone number, email, price, name

### Improve Labels
when labels are necessary, improve them by combining them with the data:
- 12 left in stock >> In stock: 12
- 3 bedrooms >> Bedrooms: 3

### Labels are Secondary
try to focus on the data instead of the label
make the label visually secondary with font size, weight and color

### When to Emphasize a Label
when there is a lot of data that is hard to get an overview over, emphasized labels can help users find what they are looking for more easily.
eg specifications of a tech product or a airbnb

## Visual vs Document Hierarchy 
a headline doesn't necessarily need to be very big
usually the content is the focus, so often titles should be small
often the visual hierarchy can look different from the semantic hierarchy
if the content speaks for itself, there might not be need for emphasizing a title (or for the title at all)

## Changing Emphasis of Non-Text Elements
icons can't be de-emphasized by changing the 'weight', like with font
changing the constrast of elements is a good way to do this
this works well for elements that have a fixed size, like dividers or icons
but making a divider or border larger and using lighter contrast can keep the 'softer' appearence without making it barely visible

## Actions
actions could be categorized by the following system:
- primary actions
	- obvious
	- solid (button with background), high contrast background colors
- secondary actions
	- clear, but not prominent
	- outline styles or lower contrast backgrounds
- tertiary actions
	- discoverable, but unbostrusive
	- stying like links, color but no background

### Destructive Actions
if a destructive action isn't the main action, secondary or tertiary button designs might work better. combine this with a confirmation step where the destructive action is the main focus


# Process
## Starting from Scratch
use a thick sharpy on a piece of paper to desing the basic layout
this forces you not to obsess over little details like boxshadows, font choices or colors

try to hold back on color
design in grayscale first, so spacing, contrast and size can decide the hierarchy of elements
it's easy to enhance a well-designed interface with color later

only put something in your design if it is a necessary component
if something is only 'nice to have' assume that building it is complex and might not be possible at this stage, so try to keep things like these out of your early designs

