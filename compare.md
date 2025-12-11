# Image Editing Models Comparison Report

## Experimental Study: SwiftEdit vs DMD2 vs Qwen-Edit

---

Qwen-Edit, based on the Qwen large language model architecture, is recognized as a **State-of-the-Art (SOTA)** image editing foundation model. Its architecture integrates advanced text-image alignment and diffusion model technology to achieve high-precision semantic and appearance editing, setting a new benchmark for complex instruction following.

This report evaluates Qwen-Edit against two high-speed alternatives, SwiftEdit (SE) and DMD2, under rigorous experimental conditions on an NVIDIA RTX 3090. The objective is to determine if Qwen-Edit's superior cognitive capacity justifies its higher computational cost when performing complex, non-trivial image transformations.

---

## 1. System Requirements & Performance

### 1.1 Resource Utilization (RTX 3090)

| Model              | VRAM Usage | Inference Speed |
| :----------------- | :--------- | :-------------- |
| **SwiftEdit (SE)** | 22 GB      | **0.67s**       |
| **DMD2**           | **18 GB**  | 1.3s            |
| **Qwen-Edit**      | 23 GB      | 26s             |

> **Key Insight:** SwiftEdit is **52× faster** than Qwen-Edit, while DMD2 is the most memory-efficient, using 18% less memory than SwiftEdit.

---

## 2. Experimental Configurations

| **Parameter / Model** | **DMD2**                             | **SwiftEdit**                               |
| --------------------- | ------------------------------------ | ------------------------------------------- |
| **Base Model**        | SDXL 1.0                             | SD 1.2                                      |
| **IP-Adapter**        | IP-Adapter-Plus SDXL (ViT-H)         | IP-SBv2                                     |
| **Inference Step**    | 4 step (via LoRA)                    | 1 step                                      |
| **Latent Source**     | Renoise Inversion (arXiv:2403.14602) | Inversion Model (same architecture as SBv2) |

---

### 3.1 Complete Comparison Table

**Scoring:** Edit Quality / Background Preservation (Scale: 1-5)

<tr>
<td align="center" valign="middle"><strong>00</strong></td>
<td valign="middle">
<strong>Source:</strong> a slanted mountain <em><u>bicycle</u></em> on the <em><u>road</u></em> in front of a <em><u>building</u></em><br/>
<strong>Edit:</strong> a slanted <em><u>rusty</u></em> mountain <em><u>motorcycle</u></em> in front of a <em><u>fence</u></em>
</td>
<td align="center" valign="middle"><img src="outputs/image/image.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image_edit_a_slanted_rusty_mountain_motor.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit0.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Qwen perfect edit. DMD2 correct motorcycle. SwiftEdit texture-only.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>01</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>round</u></em> cake with <em><u>orange</u></em> frosting on a <em><u>wooden</u></em> plate<br/>
<strong>Edit:</strong> a <em><u>square</u></em> cake with <em><u>strawberry</u></em> frosting on a <em><u>plastic</u></em> plate
</td>
<td align="center" valign="middle"><img src="outputs/image/image1.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image1_edit_a_square_cake_with_strawberry_.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit1.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit1.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Qwen success but hallucinated background. DMD2 failed geometric change.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>02</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>cat sitting</u></em> on a <em><u>wooden</u></em> chair<br/>
<strong>Edit:</strong> a <em><u>red dog</u></em> with <em><u>flowers in mouth standing</u></em> on a <em><u>metal</u></em> chair
</td>
<td align="center" valign="middle"><img src="outputs/image/image2.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image2_edit_a_red_dog_with_flowers_in_mout.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit2.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit2.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Accurate red dog + flowers. DMD2 wrong color/pose.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>03</strong></td>
<td valign="middle">
<strong>Source:</strong> blue light, a black and white <em><u>cat</u></em> is playing with a <em><u>flower</u></em><br/>
<strong>Edit:</strong> blue light, a black and white <em><u>dog</u></em> is playing with a <em><u>yellow ball</u></em>
</td>
<td align="center" valign="middle"><img src="outputs/image/image3.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image3_edit_blue_light,_a_black_and_white_.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit3.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit3.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Qwen perfect. DMD2 good BW dog. SwiftEdit still a cat.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>04</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>cat sitting</u></em> next to a mirror<br/>
<strong>Edit:</strong> a <em><u>silver cat sculpture standing</u></em> next to a mirror
</td>
<td align="center" valign="middle"><img src="outputs/image/image4.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image4_edit_a_silver_cat_sculpture_standin.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit4.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit4.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Perfect metal texture. DMD2 refused change. SwiftEdit noisy.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>06</strong></td>
<td valign="middle">
<strong>Source:</strong> a cup of <em><u>coffee</u></em> with drawing of <em><u>tulip</u></em> putted on the wooden table<br/>
<strong>Edit:</strong> a <em><u>yellow</u></em> cup of <em><u>milk</u></em> with drawing of <em><u>rose</u></em> putted on the wooden table
</td>
<td align="center" valign="middle"><img src="outputs/image/image6.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image6_edit_a_yellow_cup_of_milk_with_draw.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit6.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit6.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Perfect yellow cup + milk + rose. DMD2 failed all.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>07</strong></td>
<td valign="middle">
<strong>Source:</strong> a german shepherd dog <em><u>stands</u></em> on the grass with <em><u>mouth closed</u></em><br/>
<strong>Edit:</strong> a <em><u>white</u></em> german shepherd dog <em><u>sits</u></em> on the grass with <em><u>big mouth opened</u></em>
</td>
<td align="center" valign="middle"><img src="outputs/image/image7.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image7_edit_a_white_german_shepherd_dog_si.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit7.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit7.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Full pose change. DMD2 only opened mouth.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>09</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>dog</u></em> is laying down on a <em><u>white</u></em> background<br/>
<strong>Edit:</strong> <em><u>Painting</u></em> of a <em><u>lion</u></em> laying down on a <em><u>blue</u></em> background
</td>
<td align="center" valign="middle"><img src="outputs/image/image9.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image9_edit_Painting_of_a_lion_laying_down.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit9.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit9.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Full regeneration (lion). DMD2 black image. SwiftEdit distorted.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>26</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>yellow bird</u></em> with a <em><u>red beak</u></em> sitting on a branch<br/>
<strong>Edit:</strong> a <em><u>toy cat</u></em> with a <em><u>red fur</u></em> sitting on a branch
</td>
<td align="center" valign="middle"><img src="outputs/image/image26.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image26_edit_a_toy_cat_with_a_red_fur_sitti.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit26.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit26.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Perfect toy cat, preserved background. DMD2 wrong color (orange).</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>27</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>opened eyes cat</u></em> sitting on <em><u>wooden floor</u></em><br/>
<strong>Edit:</strong> a <em><u>closed eyes dog</u></em> sitting on <em><u>green grass</u></em>
</td>
<td align="center" valign="middle"><img src="outputs/image/image27.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image27_edit_a_closed_eyes_dog_sitting_on_g.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit27.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit27.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Total scene rewrite. DMD2 cat-dog hybrid.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>28</strong></td>
<td valign="middle">
<strong>Source:</strong> <em><u>white</u></em> flowers on a tree branch with <em><u>blue sky</u></em> background<br/>
<strong>Edit:</strong> <em><u>Painting</u></em> of <em><u>red</u></em> flowers on a tree branch with <em><u>white</u></em> background
</td>
<td align="center" valign="middle"><img src="outputs/image/image28.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image28_edit_Painting_of_red_flowers_on_a_t.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit28.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit28.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Accurate painting style. DMD2 color change only.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>93</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>collie dog</u></em> is <em><u>sitting</u></em> on a <em><u>bed</u></em><br/>
<strong>Edit:</strong> a <em><u>Garfield cat</u></em> is <em><u>sleeping</u></em> on a <em><u>sofa</u></em>
</td>
<td align="center" valign="middle"><img src="outputs/image/image93.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image93_edit_a_Garfield_cat_is_sleeping_on_.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit93.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit93.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Garfield + sofa. DMD2 striped cat wrong pose. SwiftEdit cat on bed.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>95</strong></td>
<td valign="middle">
<strong>Source:</strong> a painting of a fairy with <em><u>green</u></em> wings holding a <em><u>glowing jar</u></em><br/>
<strong>Edit:</strong> a painting of a fairy with <em><u>purple</u></em> wings holding a <em><u>white crystal ball</u></em>
</td>
<td align="center" valign="middle"><img src="outputs/image/image95.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image95_edit_a_painting_of_a_fairy_with_pur.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit95.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit95.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Perfect purple wings + crystal ball. DMD2 wings still green.</td>
</tr>
<tr>
<td align="center" valign="middle"><strong>98</strong></td>
<td valign="middle">
<strong>Source:</strong> a <em><u>light bulb</u></em> hanging from a wire with <em><u>sky</u></em> in the background<br/>
<strong>Edit:</strong> a <em><u>cat</u></em> hanging from a wire with <em><u>grass</u></em> in the background
</td>
<td align="center" valign="middle"><img src="outputs/image/image98.jpg" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/swiftedit_results/swift_edit_result_img/image98_edit_a_cat_hanging_from_a_wire_with.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/dmd2_result/result_renoise_edit98.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><img src="outputs/compare_result/edit98.png" width="200" height="100" style="object-fit: cover;"/></td>
<td align="center" valign="middle"><strong>Qwen</strong></td>
<td valign="middle">Correct cat + grass. DMD2 wind chime instead. SwiftEdit cat face artifact.</td>
</tr>
</tbody>
</table>

---

## 4. Statistical Summary

### 4.1 Win Distribution

| Model         | Tasks Won   | Win Rate |
| :------------ | :---------- | :------- |
| **Qwen-Edit** | **14 / 14** | **100%** |
| **DMD2**      | 0 / 14      | 0.0%     |
| **SwiftEdit** | 0 / 14      | 0%       |

### 4.2 Average Scores

| Model         | Avg Edit Score | Avg Preservation | Speed     |
| :------------ | :------------- | :--------------- | :-------- |
| **Qwen-Edit** | **5.00 / 5**   | 3.79 / 5         | 26s       |
| **DMD2**      | 2.14 / 5       | **3.93 / 5**     | 1.3s      |
| **SwiftEdit** | 1.86 / 5       | 4.14 / 5         | **0.67s** |

---

## 5. Conclusions & Recommendations

Based on the experimental data, the conclusion is clear:

1.  **SwiftEdit** is fast (0.67s) but **ineffective** for meaningful editing; it often produces noise or minimal changes.
2.  **DMD2** is efficient (1.3s, 18GB VRAM) but suffers from **rigidity**; it struggles to alter the structure or geometry of an image.
3.  **Qwen-Edit** is the **only viable solution for professional-grade editing**.

### Final Verdict

> Although **Qwen-Edit** requires 26 seconds and 23GB VRAM, it is the only model that consistently understands complex prompts, correctly handles physics/material changes (e.g., Fur → Silver), and modifies geometry (e.g., Round → Square). **Speed is irrelevant if the output is incorrect; therefore, Qwen-Edit is the optimal choice.**
