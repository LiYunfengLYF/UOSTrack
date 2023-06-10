#  Sample Imbalance Adjustment and Similar Object Exclusion in Underwater Object Tracking

## Our method

Our manuscript.


## Underwater images and Open-air sequences Hybrid Training
### Prepare Dataset

Download RUOD(https://github.com/dlut-dimt/RUOD)

Download fish dataset1(https://universe.roboflow.com/pafd/fish-clean) and fish dataset2(https://public.roboflow.com/object-detection/fish)

Merge fish dataset1 and fish dataset2. Then you get FishExtend dataset. Tools are in `./tracking/tools/`

RUOD and FishExtend should look like:

   ```
   ${PROJECT_ROOT}
    -- data
        -- RUOD
            |-- annotations
            |-- images
        -- FishExtend
            |-- annotations
            |-- images
   ```

### Modify Path

Go to `lib/train/admin/local.py` to set datasets dir

Then you can training tracker follow OSTrack paradigm

## Test

### Prepare Dataset

Download UOT100(https://www.kaggle.com/datasets/landrykezebou/uot100-underwater-object-tracking-dataset)

Download UTB180(https://www.kaggle.com/datasets/bastech/utb180)

Put UOT100 and UTB in ./data. It should look like:

   ```
   ${PROJECT_ROOT}
    -- data
        -- UOT100
            |-- AntiguaTurtle
            |-- ArmyDiver1
            |-- ArmyDiver2
            ...
        -- UTB180
            |-- Video_0001
            |-- Video_01
            |-- Video_0002
            ...
   ```

### Modify Path
Go to `lib/test/evaluation/local.py` to set datasets dir

### Model

[Checkpoints](https://drive.google.com/drive/folders/1rfD-axPbJgOJCy378vpK0RROb9-QvowH?usp=share_link) will be found here.

Put them to `./output/checkpoints/train/ostrack`

### using MBPP
Go to `lib/test/tracker/ostrack.py`. Then set use MDPP is True
   ```
        # using kalman filter to head        
        # TODO 
        self.use_kf = False  # True
   ```

### using Underwater Image Enhancement method 
Download UIE [model](https://drive.google.com/drive/folders/1wsDRj5CF-UKdX7V6WYrdm87pUzpGoIAn?usp=sharing)
Merge it with `external/uie`
Go to `lib/test/tracker/ostrack.py`. Then set use_uie is True
   ```
        # using kalman filter to head        
        # TODO 
        self.use_uie = False  # True
        self.uie = build_fuinegan() # RGHSUWE, UCM, build_shallowuwnet(), build_ushape()
   ```

## Evaluation

[Raw results](https://drive.google.com/drive/folders/1FF8_GP06smyYQ8uMHB0TDLhM3L9jASQi?usp=share_link) can be found here.

- UOT100

Put the UOT100 raw results  on `$PROJECT_ROOT$/output/test/tracking_results/`
```
python tracking/analysis_results.py # need to modify tracker configs and names
```
- UTB180

Put the UTB1180 raw results  on `$PROJECT_ROOT$/output/test/tracking_results/`

```
python tracking/analysis_results.py # need to modify tracker configs and names
```


## Acknowledgments
* Thanks for the [OSTrack](https://github.com/botaoye/OSTrack) library, which helps us to quickly implement our ideas.
