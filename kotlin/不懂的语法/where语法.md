# where
fun <T> register(view: T) where T : View, T : LifecycleObserver? {
    // we need to wait until view is mounted in the hierarchy as this method is called only at the
    // moment of the view creation. In order to register lifecycle observer we need to find ancestor
    // of type Screen and this can only happen when the view is properly attached. We rely on
    // Android's onLayout callback being triggered when the view gets added to the hierarchy and
    // only then we attempt to locate lifecycle owner ancestor.
    view.addOnLayoutChangeListener(mRegisterOnLayoutChange)
}
意思就是T泛型
必须满足 View，LifecycleObserver类型