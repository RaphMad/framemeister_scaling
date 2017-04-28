# Scaling to full screen:

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
  - modify `ZOOM_WIDTH` until picture fills horizontal space
  - modify `ZOOM_H_POS` to align horizontally
5. use `VISUAL` settings to mask or reveal horizontal pixels, should only need `ZOOM_WIDTH`, `H_WIDTH` and `ZOOM_H_POS`

# Integer scaling:

- (+)
  - Keeps aspect ratio
  - Integer scale - pixels are exactly represented
- (-)
  - Either hides some rows in the top/bottom overlay area or has to use a letterbox
  - Hard to setup


1. Modify `VISUAL_SET` until picture is cropped correctly
2. Modify `ZOOM_SET` until horizontal and vertical scales are integer
  - Use `ZOOM_SIZE`, `ZOOM_OVERSCAN` and `ZOOM_V_POS` first to achieve vertical integer scaling
  - Then use `ZOOM_WIDTH` to also achieve horizontal integer scaling (see reasoning below)

 ```
 target-Y-res = input-Y-res * ZOOM_SIZE * ZOOM_OVERSCAN * V_WIDTH
 target-X-res = input-X-res * ZOOM_SIZE * ZOOM_OVERSCAN * ZOOM_WIDTH * H_WIDTH
 ```


- Is exact integer even possible considering pixels need to be cropped?
> Yes, reasoning:
> - `V_WIDTH` and `H_WIDTH` are constant since they are used for cropping
> - `ZOOM_SIZE` and `ZOOM_OVERSCAN` are variable, but used in both calculations, so they need to be set first and can be used to get vertical resolution to integer scale
> - `ZOOM_WIDTH` then is the independent "knob" that allows to also get horizontal resolution to integer scale

- Open questions:
  - Which values for `input-Y-res`/`input-X-res` for which PAL console?
  - How to verify? - Needs coefficients for `ZOOM_SIZE` etc. to actually calculate it
