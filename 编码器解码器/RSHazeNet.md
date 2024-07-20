```python
RSHazeNet(
  (patch_embed_level_1): OverlapPatchEmbed(
    (proj): Conv2d(3, 32, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
  )
  (skip_connection_level_1_pre): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(8, 8, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(8, 8, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=8)
      (conv_5): Conv2d(8, 8, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=8)
      (conv_7): Conv2d(8, 8, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=8)
      (mlp): Sequential(
        (0): Conv2d(32, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(128, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (skip_connection_level_1_post): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(8, 8, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(8, 8, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=8)
      (conv_5): Conv2d(8, 8, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=8)
      (conv_7): Conv2d(8, 8, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=8)
      (mlp): Sequential(
        (0): Conv2d(32, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(128, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (down_level_2): Downsample(
    (body): Sequential(
      (0): Conv2d(32, 16, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
      (1): PixelUnshuffle()
    )
  )
  (skip_connection_level_2_pre): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(16, 16, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(16, 16, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=16)
      (conv_5): Conv2d(16, 16, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=16)
      (conv_7): Conv2d(16, 16, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=16)
      (mlp): Sequential(
        (0): Conv2d(64, 256, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(256, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (skip_connection_level_2_mid): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(16, 16, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(16, 16, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=16)
      (conv_5): Conv2d(16, 16, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=16)
      (conv_7): Conv2d(16, 16, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=16)
      (mlp): Sequential(
        (0): Conv2d(64, 256, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(256, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (skip_connection_level_2_post): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(16, 16, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(16, 16, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=16)
      (conv_5): Conv2d(16, 16, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=16)
      (conv_7): Conv2d(16, 16, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=16)
      (mlp): Sequential(
        (0): Conv2d(64, 256, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(256, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (down_level_3): Downsample(
    (body): Sequential(
      (0): Conv2d(64, 32, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
      (1): PixelUnshuffle()
    )
  )
  (skip_connection_level_3_pre): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(32, 32, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=32)
      (conv_5): Conv2d(32, 32, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=32)
      (conv_7): Conv2d(32, 32, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=32)
      (mlp): Sequential(
        (0): Conv2d(128, 512, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(512, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
    (1): BasicBlock(
      (conv_1): Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(32, 32, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=32)
      (conv_5): Conv2d(32, 32, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=32)
      (conv_7): Conv2d(32, 32, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=32)
      (mlp): Sequential(
        (0): Conv2d(128, 512, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(512, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (skip_connection_level_3_post): Sequential(
    (0): BasicBlock(
      (conv_1): Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(32, 32, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=32)
      (conv_5): Conv2d(32, 32, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=32)
      (conv_7): Conv2d(32, 32, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=32)
      (mlp): Sequential(
        (0): Conv2d(128, 512, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(512, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
    (1): BasicBlock(
      (conv_1): Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1))
      (conv_3): Conv2d(32, 32, kernel_size=(3, 3), stride=(1, 1), padding=(3, 3), dilation=(3, 3), groups=32)
      (conv_5): Conv2d(32, 32, kernel_size=(5, 5), stride=(1, 1), padding=(6, 6), dilation=(3, 3), groups=32)
      (conv_7): Conv2d(32, 32, kernel_size=(7, 7), stride=(1, 1), padding=(9, 9), dilation=(3, 3), groups=32)
      (mlp): Sequential(
        (0): Conv2d(128, 512, kernel_size=(1, 1), stride=(1, 1), bias=False)
        (1): ReLU()
        (2): Conv2d(512, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
      )
    )
  )
  (up_level_3): Upsample(
    (body): Sequential(
      (0): Conv2d(128, 256, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
      (1): PixelShuffle()
    )
  )
  (up_level_2): Upsample(
    (body): Sequential(
      (0): Conv2d(64, 128, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
      (1): PixelShuffle()
    )
  )
  (cmfi_level_1_2): CMFI(
    (norm_1): LayerNorm2d()
    (norm_2): LayerNorm2d()
    (q_1): Sequential(
      (0): Downsample(
        (body): Sequential(
          (0): Conv2d(32, 16, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
          (1): PixelUnshuffle()
        )
      )
      (1): Conv2d(64, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    )
    (v_1): Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (k_2): Conv2d(64, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (v_2): Conv2d(64, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (proj_1): Conv2d(64, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (proj_2): Conv2d(32, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
  )
  (cmfi_level_2_3): CMFI(
    (norm_1): LayerNorm2d()
    (norm_2): LayerNorm2d()
    (q_1): Sequential(
      (0): Downsample(
        (body): Sequential(
          (0): Conv2d(64, 32, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
          (1): PixelUnshuffle()
        )
      )
      (1): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
    )
    (v_1): Conv2d(64, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (k_2): Conv2d(128, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (v_2): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (proj_1): Conv2d(128, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (proj_2): Conv2d(64, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
  )
  (ifte_level_2): IFTE(
    (norm_dec): LayerNorm2d()
    (norm_skip): LayerNorm2d()
    (qk_avg_pool): AdaptiveAvgPool2d(output_size=1)
    (qk): Conv2d(128, 128, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (v): Conv2d(128, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (proj_out): Conv2d(64, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
  )
  (ifte_level_1): IFTE(
    (norm_dec): LayerNorm2d()
    (norm_skip): LayerNorm2d()
    (qk_avg_pool): AdaptiveAvgPool2d(output_size=1)
    (qk): Conv2d(64, 64, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (v): Conv2d(64, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
    (proj_out): Conv2d(32, 32, kernel_size=(1, 1), stride=(1, 1), bias=False)
  )
  (output_level_1): Conv2d(32, 4, kernel_size=(3, 3), stride=(1, 1), padding=(1, 1), bias=False, padding_mode=reflect)
)
```

