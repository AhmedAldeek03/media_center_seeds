# Media center: Seeds UI cards

A companion recipe for [Media center](https://github.com/AhmedAldeek03/media_center_recipe).
It renders the **Card** view mode of News and Event with the Seeds UI card component
(`seeds_ui:seeds_ui_card`), so listings match the rest of a Seeds site.

Only the Card view mode changes. Content types, fields, views and the Default view mode stay
as Media center sets them up.

## What it does

- Applies the Media center recipe first, if it hasn't been applied yet
- Installs Display Suite, UI Patterns and UI Patterns Layouts, and the Seeds UI theme
  (it does not make Seeds UI the default theme)
- Switches the News and Event **Card** displays to the Seeds UI card layout:

| Card slot | News                    | Event                                    |
|-----------|-------------------------|------------------------------------------|
| Image     | Featured image (linked) | Featured image (linked)                  |
| Title     | Title                   | Title                                    |
| Body      | Summary                 | Date and time, location, summary         |
| Link      | "Read more"             | "Read more"                              |

Card options: `article` wrapper, image zoom on hover, 12px rounded corners, dark text,
no background overlay. Change them under the Card display's layout settings.

## Requirements

- Drupal 11
- Media center (`drupal/media_center_recipe`)
- Seeds UI, Display Suite and UI Patterns 2

## Installation

Both recipes are on GitHub for now, so add both repositories first:

```bash
composer config repositories.media_center_recipe vcs https://github.com/AhmedAldeek03/media_center_recipe
composer config repositories.media_center_seeds vcs https://github.com/AhmedAldeek03/media_center_seeds
composer require drupal/media_center_seeds:1.0.x-dev@dev
drush recipe ../recipes/media_center_seeds
drush cache:rebuild
```

With DDEV, put `ddev` before each command.

## Notes

- **Styling comes from your Seeds subtheme.** The Seeds UI base theme ships the card markup
  (`card-default`, `card-default-image`, …) but almost no CSS; each Seeds site styles it in
  its own subtheme.
- **The title is not a link.** Drupal always adds the node's Title to the render array under
  the key `title`, and core fills the component's `title` slot from it. Placing a linked title
  there as well would print it twice, so the card uses the node's own Title. The image and the
  "Read more" link both go to the full page.
- **Do not enable UI Patterns Settings 2.x.** Seeds UI pulls it in through Composer, but
  version 2.4 is built for UI Patterns 1.x and breaks every page when enabled alongside
  UI Patterns 2. This recipe does not enable it, and does not need it.
