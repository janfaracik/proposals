# Cards

Use cards to surface related information and controls to users.

![Cards](cards.png)

## Background

⚠️Draft ⚠️

Currently in Jenkins we show lots of information in job/build screens

This currently takes up lots of vertical space, but little horizontal

we also have really long sidebars, with lots of links, sometimes the same link multiple times

these summary items arent very visual, or consistent, or give much information

## Proposal

proposal is a new cards system, which automaticlaly resizes to different screen sizes, from smallest to largest

cards can show more info, more visual

cards will have a consistent set of components that can be reused, or developers can add their own

theyll ahve a consistent action row in the top right, same for every card

theyre interactive

theyre expandable

theyre customizable

## Questions

* Should the widgets be of fixed size or do we have a grid where a widget can fill 1x1, 2x1, or whatever number of cells?

Current thinking for MVP is no due to complexities of ordering/adjusting for different screen resolutions.

* Can we rearrange the widgets?

For an MVP I don't think so, but it's definitely something that'd be interesting for the future.

* Can we customize the appearance (order, visibility, size, color)?

Yes to all of the above.

Developers should be able to define priorities for their cards, e.g. the pipeline graph view or console would probably take highest priority.

Visibility, size and color should all be customizable too - e.g. the console view could follow your text editor theme.

* Does the layout adapt to different screen sizes automatically?

Yes, cards and their contents should scale to different screen sizes.
