# CityScapes

```json
{
    "name": "PSPNet",
    "n_gpu": 1,
    "use_synch_bn": false,

    "arch": {
        "type": "PSPNet",
        "args": {
            "backbone": "resnet50",
            "freeze_bn": false,
            "freeze_backbone": false
        }
    },

    "train_loader": {
        "type": "CityScapes",
        "args":{
            "data_dir": "./data/cityscapes",
            "batch_size": 32,
            "base_size": 400,
            "crop_size": 380,
            "augment": true,
            "shuffle": true,
            "scale": true,
            "flip": true,
            "rotate": true,
            "blur": false,
            "split": "train",
            "num_workers": 4
        }
    },

    "val_loader": {
        "type": "CityScapes",
        "args":{
            "data_dir": "./data/cityscapes",
            "batch_size": 8,
            "crop_size": 480,
            "val": true,
            "split": "val",
            "num_workers": 4
        }
    },

    "optimizer": {
        "type": "SGD",
        "differential_lr": true,
        "args":{
            "lr": 0.01,
            "weight_decay": 1e-4,
            "momentum": 0.9
        }
    },

    "loss": "CrossEntropyLoss2d",
    "ignore_index": 255,
    "lr_scheduler": {
        "type": "Poly",
        "args": {}
    },

    "trainer": {
        "epochs": 20,
        "save_dir": "saved/",
        "save_period": 10,
  
        "monitor": "max Mean_IoU",
        "early_stop": 10,
        
        "tensorboard": true,
        "log_dir": "saved/runs",
        "log_per_iter": 20,

        "val": true,
        "val_per_epochs": 5
    }
}
```



# ade20k

```
{
    "name": "PSPNet",
    "n_gpu": 1,
    "use_synch_bn": false,

    "arch": {
        "type": "PSPNet",
        "args": {
            "backbone": "resnet50",
            "freeze_bn": false,
            "freeze_backbone": false
        }
    },

    "train_loader": {
        "type": "ADE20K",
        "args":{
            "data_dir": "./data/ADEChallengeData2016",
            "batch_size": 16,
            "base_size": 400,
            "crop_size": 380,
            "augment": true,
            "shuffle": true,
            "scale": true,
            "flip": true,
            "rotate": true,
            "blur": false,
            "split": "training",
            "num_workers": 2
        }
    },

    "val_loader": {
        "type": "ADE20K",
        "args":{
            "data_dir": "./data/ADEChallengeData2016",
            "batch_size": 8,
            "crop_size": 480,
            "val": true,
            "split": "validation",
            "num_workers": 2
        }
    },

    "optimizer": {
        "type": "SGD",
        "differential_lr": true,
        "args":{
            "lr": 0.01,
            "weight_decay": 1e-4,
            "momentum": 0.9
        }
    },

    "loss": "CrossEntropyLoss2d",
    "ignore_index": 255,
    "lr_scheduler": {
        "type": "Poly",
        "args": {}
    },

    "trainer": {
        "epochs": 20,
        "save_dir": "saved/",
        "save_period": 10,
  
        "monitor": "max Mean_IoU",
        "early_stop": 10,
        
        "tensorboard": true,
        "log_dir": "saved/runs",
        "log_per_iter": 20,

        "val": true,
        "val_per_epochs": 5
    }
}
```







Epoch:200

The best val loss:0.10093951739113906
saving model with val_loss 0.1009

The last: Train Loss: 0.1076, Valid Loss: 0.1016
