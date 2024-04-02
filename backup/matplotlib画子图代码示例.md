## subplot画子图
```python
for index,n in enumerate(imgName):
    plt.subplot(params["batch_size"],params["batch_size"],index*3+1,title="Input" if index==0 else "")
    plt.imshow(x[index].transpose(0,1).transpose(1,2).contiguous())
    plt.axis("off") # 去掉 x y轴
    plt.subplot(params["batch_size"],params["batch_size"],index*3+2,title="GT)
    plt.imshow(y[index],cmap="gray")
    plt.axis("off")
    plt.subplot(params["batch_size"],params["batch_size"],index*3+3,title="Mask")
    plt.imshow(mask[index],cmap="gray")
    plt.axis("off")
    # plt.subplots_adjust(left=0.027,
    #                     bottom=0,
    #                     right=0.99,
    #                     top=0.93,
    #                     wspace=0.005,
    #                     hspace=0.045)
    fig.tight_layout()
```

## subplots画子图

```python
fig,axes=plt.subplots(params["batch_size"],params["batch_size"])
for index,n in enumerate(imgName):
    axes[index,0].imshow(x[index].transpose(0,1).transpose(1,2).contiguous())
    axes[index, 0].axis("off")
    axes[index,1].imshow(y[index],cmap="gray")
    axes[index, 1].axis("off")
    axes[index,2].imshow(mask[index],cmap="gray")
    axes[index, 2].axis("off")
    axes[0,0].set_title("Input")
    axes[0,1].set_title("GT")
    axes[0,2].set_title("Mask")
    plt.subplots_adjust(left=0.027,
                            bottom=0,
                            right=0.99,
                            top=0.93,
                            wspace=0.005,
                            hspace=0.045)
```
