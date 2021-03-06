# Changelog

## Next version: 0.9.1

No change yet

## 0.9.0

### New features

- Add generic `ScrollView` wrapper. Removes internal scrolling behaviour from
  `TextView`.
- Callbacks sent through `Cursive::cb_sink()` are now processed instantly,
  without the need for `set_fps`.
- Make backend a dynamic choice
    - User must select a backend in `Cursive::new`
    - 3rd party libraries do not need to play with backend features anymore
- Move from `chan` and `chan-signals` to `crossbeam-channel` and `signal-hook`
- Batch-process events for higher performance
- Add `StackView::find_layer_from_id`
- Add `SelectView::insert_item`
- Add `TextArea::{enable, disable}`
- Reworked `AnyView`
- `SelectView`: Fix mouse events
- Return callbacks from manual control methods
    - `SelectView::{set_selection, select_up, select_down, remove_item}`
    - `EditView::{set_content, insert, remove}`
- Add `rect::Rect`

### Changes

- Renamed `Vec4` to `Margins`
- `Callbacks` cannot be created from functions that return a value
    - The returned value used to be completely ignored
- `AnyView` does not extend `View` anymore (instead, `View` extends `AnyView`)
    - If you were using `AnyView` before, you probably need to replace it with `View`
- Scrolling is now added to a view with `.scrollable()`
- `cb_sink` is now a `crossbeam_channel::Sender` instead of `chan::Sender`
- `SelectView::selection` now returns an `Option<Rc<T>>` instead of just `Rc<T>`.
   It will return `None` if the `SelectView` is empty.


## 0.8.1

### New features

- Add `Cursive::clear_global_callbacks`

### Bugfixes

- Fix non-ASCII input with pancurses backend
- Fix `StackView::move_layer`
- Fix layout computation for `SelectView`
- Remove unused `maplit` dependency for termion and blt backends

## 0.8.0

### New features

- Style (breaking change):
    - Added support for bold/italic/underlined text
    - Added `StyledString` for markup text
    - Refactored line-break module
- Colors (breaking change):
    - Added ColorStyle and PaletteColor for more flexible colored text
- Buttons:
    - Added `Dialog::buttons` to iterate on buttons
    - Added `Button::set_label` and `Button::label`
- TextView:
    - Added TextContent, a way to separate model and view for TextView
    - Added manual scrolling methods
- Allow multiple global callbacks per event
- Allow buttons and delimiters in top-level menubar
- StackView:
    - Added `StackView::move_layer` to re-order layers
    - `StackView::pop_layer` now returns the pop'ed view
    - Added `StackView::reposition_layer` to move a layer around
- Dialog: added `Dialog::focus(&self)`
- SelectView: added `SelectView::selected`
- `Cursive::cb_sink` now accepts `FnOnce` (previously `Fn` only)

### Bugfixes

- Fix a bug in `TextArea::set_content`
- Fix `Color::from_256colors` for grayscale colors
- Fix resize detection on windows
- Fix possible panic with weird input on pancurses
- Fix possible panic in ListView layout

### Doc

- Add per-distributions instructions to install ncurses
- Improved comments in examples
- Improve doc for `Cursive::find_id`
- Improve doc for `Identifiable::with_id`
- Include Changelog
