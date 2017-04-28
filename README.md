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
   - modify `ZOOM_WIDTH` until aspect ratio is restored


- Open questions:
   - What's the difference between using `ZOOM_H_POS` vs. `H_POS` (also for `ZOOM_V_POS` vs. `V_POS`)?
   - How to verify correct aspect ratio?

# Integer scaling:

- (+)
  - Integer scale - pixels are exactly represented
  - Keeps aspect ratio
- (-)
  - Either hides some lines in the top/bottom overlay area or has to use a letterbox
  - Hard to setup


1. Modify `VISUAL_SET` until picture is cropped correctly
2. Modify `ZOOM_SET` until horizontal and vertical scales are integer
   - Use `ZOOM_SIZE`, `ZOOM_OVERSCAN` and `ZOOM_V_POS` first to achieve vertical integer scaling
   - Then use `ZOOM_WIDTH` to also achieve horizontal integer scaling (see reasoning below)

 ```
 target-Y-res = input-Y-res * ZOOM_SIZE * ZOOM_OVERSCAN * V_WIDTH
 target-X-res = input-X-res * ZOOM_SIZE * ZOOM_OVERSCAN * ZOOM_WIDTH * H_WIDTH
 ```


> Reasoning:
> - `V_WIDTH` and `H_WIDTH` are constant since they are used for console-individual cropping
> - `ZOOM_SIZE` and `ZOOM_OVERSCAN` are variable, but used in both calculations, so Y res has to be set first
> - `ZOOM_WIDTH` then is the independent "knob" that allows to also get an integer X res

- Open questions:
  - Which values for `input-Y-res`/`input-X-res` for which PAL console?
  - How to verify? - Needs coefficients for the configured `ZOOM_SIZE`, `ZOOM_WIDTH`, ... values to actually calculate it
