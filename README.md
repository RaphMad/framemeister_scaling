# Settings that affect scaling:

- `H_WIDTH`
   - Defines the size of the horizontal part of the input signal that will be processed
   - Can be used to crop the input signal (in combination with `H_POS`)
- `V_WIDTH`
   - Defines the size of the vertical part of the input signal that will be processed
   - Can be used to crop the input signal (in combination with `V_POS`)
- `ZOOM_SIZE`
   - Zooms uniformely, keeps aspect ratio
   - Does not affect the black bars to the left and right
- `ZOOM_WIDTH`
   - Zooms only in horizontal direction, modifies aspect ratio
   - Changes the size of the black bars the left and right
- `ZOOM_OVERSCAN`
   - Shrinks the picture uniformely
   - Affects the black bars to the left and right


# Scaling to full height:

- (+)
  - Uses as much screen space as possible
  - Keeps aspect ratio
  - (Relatively) easy to setup
- (-)
  - Non-integer scale - pixels are not exactly represented


1. `ZOOM ON`
2. set `ZOOM_SIZE` to `100%`
3. vertical scaling:
   - reduce `ZOOM_SIZE` until picture fills vertical space
   - modify `ZOOM_V_POS` to align vertically
4. horizontal scaling:
   - use `H_WIDTH` and `ZOOM_H_POS` until picture is cropped correctly
   - modify `ZOOM_WIDTH` until aspect ratio is restored (measure manually)


# Integer scaling:

- (+)
  - Integer scale - pixels are exactly represented
  - Keeps aspect ratio
- (-)
  - Either loses some lines in the top/bottom area or has to use a letterbox
  - Hard to setup


1. Modify `VISUAL_SET` until picture is cropped correctly
2. Modify `ZOOM_SET` and/or `ZOOM_OVERSCAN` until vertical scale is integer
   - Can use scanlines to verify this
   - May need to go back and slightly modify `V_WIDTH` to get perfect results
3. Align picture vertically using `ZOOM_V_POS`
4. Modify `ZOOM_SIZE` until horizontal scale is integer
   - No method to verify this
   - Simply try to achieve the desired aspect ratio (measure manually)
5. Align picture horizontally using `ZOOM_H_POS`
