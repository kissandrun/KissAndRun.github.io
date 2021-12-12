# 最简nnUNet训练-医学影像处理入门课程


# 最简 nnUNet 训练

## 准备数据
### 获得数据

已经将大家分割的图像进行了格式整理和一些预处理，并将其存放在如下目录下![image-20210416133145262](https://i.loli.net/2021/04/16/g5FoElj8xWQuXSO.png)

![image-20210419154054646](https://i.loli.net/2021/04/19/X8eqG9ENzwyLF3g.png)

**volume**和**label**分别是原图和大家手动分割好的标签图

![image-20210419154303973](https://i.loli.net/2021/04/19/39V6qUzEKvTemCu.png)

### 创建分割任务文件夹

![image-20210416133232318](https://i.loli.net/2021/04/16/nCxsajvOpA8ydeU.png)

然后在**nnUNet_raw_data**下新建文件夹 **TaskXXX_任务名**。 **XXX**是任务序号(大于100的数，前100被占用了，不如大家就取**100** + 自己组的**id**，**比如第21组就取名Task121_任务名**)，任务名取一个好记的英文名。

最后的文件结构如下

   ```
   nnUNet_raw/nnUNet_raw_data/
   ├── Task101_BrainTumour
   ├── Task102_Heart
   ├── Task103_Liver
   ├── Task104_Hippocampus
   ├── Task105_Prostate
   ├── ...
   ```

   然后在任务文件夹里构建如下结构

   ```
   Task101_BrainTumour/
   ├── dataset.json
   ├── imagesTr
   ├── (imagesTs)
   └── labelsTr
   ```

 **imagesTr** 和 **labelsTr** 分别存放训练的原图和标签。**imagesTs**存放测试的原图（可以没有）。**dataset.json** 下面会说。旁边的**Task133_LungAirway**是一个范例，可以在根据这个进行学习和修改。

### 图像命名（可能是整个过程最难的环节）

**imagesTr** 和 **labelsTr** 中图像的命名也有要求。

其中**imagesTr**（也就是原图）需要改成类似下图这样，而且必须是 **.nii.gz** 格式。建议写个 **Python** 脚本批量重命名并保存成 **.nii.gz** 格式（**如果数量少，也可以手动修改**）。

![image-20210419154803519](https://i.loli.net/2021/04/19/n7xAYSG5mcHz1Cl.png)

**labelsTr**（也就是标签图）需要改成如下样式，注意原图和标签图序号一一对应，只是原图后面带**_0000**，而标签图不带。

![image-20210419154916117](https://i.loli.net/2021/04/19/niaxUsvmTVqlDLh.png)

### **dataset.json** 编写

上文说到这个任务文件夹应该包含一个 **dataset.json** 文件。下面是一个例子（可以在**Task133**里找到）

```json
{
    "description": "Task128_LungLobe",
    "labels": {
        "0": "0",
        "1": "1"
    },
    "licence": "see challenge website",
    "modality": {
        "0": "CT"
    },
    "name": "Task128_LungLobe",
    "numTest": 0,
    "numTraining": 7,
    "reference": "see challenge website",
    "release": "0.0",
    "tensorImageSize": "4D",
    "test": [],
    "training": [
        {
            "image": "./imagesTr/LungLobe_000.nii.gz",
            "label": "./labelsTr/LungLobe_000.nii.gz"
        },
        {
            "image": "./imagesTr/LungLobe_001.nii.gz",
            "label": "./labelsTr/LungLobe_001.nii.gz"
        },
        {
            "image": "./imagesTr/LungLobe_002.nii.gz",
            "label": "./labelsTr/LungLobe_002.nii.gz"
        },
        {
            "image": "./imagesTr/LungLobe_003.nii.gz",
            "label": "./labelsTr/LungLobe_003.nii.gz"
        },
        {
            "image": "./imagesTr/LungLobe_004.nii.gz",
            "label": "./labelsTr/LungLobe_004.nii.gz"
        },
        {
            "image": "./imagesTr/LungLobe_005.nii.gz",
            "label": "./labelsTr/LungLobe_005.nii.gz"
        },
        {
            "image": "./imagesTr/LungLobe_006.nii.gz",
            "label": "./labelsTr/LungLobe_006.nii.gz"
        }
    ]
}
```

按自己的任务的属性，修改上面的**labels**，**numTest**，**numTraining**等等信息。注意：这里**image**的文件名里没有 **_0000** 。但是修改这个**json**文件夹的工作量是比较大的，推荐写个 **Python** 脚本自动生成（**当然如果只有几张图，手动改一改也是可以的**）。下面是例子

```python
from collections import OrderedDict
from batchgenerators.utilities.file_and_folder_operations import save_json


def main():
    foldername = "Task128_LungLobe"  #训练的名称
    numTraining = 80      #训练集数量
    numTest = 6           #测试集数量
    numClass = 6          #分割的类别，如果不是多器官分割 则为2
    json_dict = OrderedDict()   
    json_dict['name'] = foldername
    json_dict['description'] = foldername
    json_dict['tensorImageSize'] = "4D"
    json_dict['reference'] = "see challenge website"
    json_dict['licence'] = "see challenge website"
    json_dict['release'] = "0.0"
    json_dict['modality'] = {
        "0": "CT",       #模态
    }
    json_dict['labels'] = {i: str(i) for i in range(numClass)}

    json_dict['numTraining'] = numTraining
    json_dict['numTest'] = numTest
    json_dict['training'] = [{'image': "./imagesTr/LungLobe_{:0>3d}.nii.gz".format(i),
                              "label": "./labelsTr/LungLobe_{:0>3d}.nii.gz".format(i)}
                             for i in range(numTraining)]

    json_dict['test'] = ["./imagesTs/LungLobe_{:0>3d}.nii.gz".format(i)
                         for i in range(numTraining, numTraining+numTest)]
    #上面的LungLobe可以换成自己的任务名
    save_json(json_dict, "./dataset.json")


if __name__ == "__main__":
    main()

```

需要发挥一点主观能动性，修改一下使之适应自己的任务。运行该脚本需要终端将目录切换到任务文件夹下，然后运行脚本。在终端输入以下命令

![image-20210407091851142](https://i.loli.net/2021/04/16/eHynPaEJzmYFuh7.png)

### 结果

![image-20210416133430514](https://i.loli.net/2021/04/16/kKQaYITosiC4NGe.png)

## 训练

1. 整理完数据，打开终端，并激活 **nnUNet** 环境，运行下面命令，

```
nnUNet_plan_and_preprocess -t XXX --verify_dataset_integrity
```

**XXX** 代替为你的任务序号。该命令进行预处理。(**需要一定时间，耐心等待**)

2. 开始训练。

单卡训练：执行

```
nnUNet_train 3d_fullres nnUNetTrainerV2 XXX 0
```

意思是对序号为**XXX**的任务进行第**0**折交叉验证，训练模式是**3d**的全像素。一共有五折交叉验证，所以最后一个数为**0-4**。
