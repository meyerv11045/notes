# Matplotlib

## Iterate through Images using Keyboard

``` python
plt.axis([-50,50,0,10000]) #[x_min, xmax, ymin,ymax]
plt.ion()
plt.show()

x = np.arange(-50, 51)
for pow in range(1,5):   # plot x^1, x^2, ..., x^4
    y = [Xi**pow for Xi in x]
    plt.clf()
    plt.axis([-50,50,0,10000]) #[x_min, xmax, ymin,ymax]
    plt.plot(x, y)
    plt.draw()
    plt.pause(0.001)

    in_ = input("Press [enter] to continue.")
    if in_.strip().lower() == 'd':
        print('deleting current image')
```

