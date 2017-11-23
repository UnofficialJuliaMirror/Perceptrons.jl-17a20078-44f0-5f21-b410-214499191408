Perceptrons.jl
======

A package with several types of Perceptron classifiers. Perceptrons are fast classifiers and can be used even for big data. Up to now, this package contains a linear perceptron for binary classification problems. However, this project will have the following perceptron classifiers: Multiclass, Kernel, Structured, Voting, Average and Sparse. Some state-of-the-art must be included after these.

[![Build Status](https://travis-ci.org/lalvim/Perceptrons.jl.svg?branch=master)](https://travis-ci.org/lalvim/Perceptrons.jl)

[![Coverage Status](https://coveralls.io/repos/lalvim/Perceptrons.jl/badge.svg?branch=master&service=github)](https://coveralls.io/github/lalvim/Perceptrons.jl?branch=master)

[![codecov.io](http://codecov.io/github/lalvim/Perceptrons.jl/coverage.svg?branch=master)](http://codecov.io/github/lalvim/Perceptrons.jl?branch=master)

Install
=======

    Pkg.add("Perceptrons")

Using
=====

    using Perceptrons

Examples
========

    using Perceptrons

    # learning a single target
    X_train        = [1.0 1.0; 0.0 1.0; 1.0 0.0; 0.0 0.0]
    Y_train        = [1; 1; 1; 1.0]
    X_test         = [.8 .9; .01 1; .9 0.2; 0.1 0.2]

    model          = Perceptrons.fit(X_train,Y_train)
    Y_test         = Perceptrons.predict(model,X_test)

    print("[Perceptron] mae error : $(mean(abs.(Y_test .- Y_pred)))")

    # if you want to save your model
    Perceptrons.save(model,filename="/tmp/perceptron_model.jld")

    # if you want to load back your model
    model = Perceptrons.load(filename="/tmp/perceptron_model.jld")


What is Implemented
======
* A fast algorithm for a linear perceptron with for a binary classification problem


What is Upcoming
=======
* Kernel Perceptron
* Multiclass Perceptron
* Voting Perceptron
* Average Perceptron
* Structured Perceptron
* Sparse Perceptron

Method Description
=======

* Perceptrons.fit - learns from input data and its related single target
    * X::Matrix{:<AbstractFloat} - A matrix that columns are the features and rows are the samples
    * Y::Vector{:<AbstractFloat} - A vector with float values.
    * copydata::Bool = true: If you want to use the same input matrix or a copy.
    * centralize::Bool = true: If you want to z-score columns. Recommended if not z-scored yet.
    * kernel::AbstractString = "rbf": If you want to apply a nonlinear Perceptron with gaussian Kernel.
    * width::AbstractFloat = 1.0: Rbf Kernel width (Only if kernel="rbf").
    * alpha::Real = 1.0e-2: learning rate.
    * shuffle_epoch::Bool = true: Shuffle dataset for each epoch. Improves convergency.
    * random_state::Int = 42: Use a seed to force same results trhough the same dataset.
    * max_epochs::Int = 5: Maximum epochs.

* Perceptrons.predict - predicts using the learnt model extracted from fit.
    * model::Perceptrons.Model - A Perceptron model learnt from fit.
    * X::Matrix{:<AbstractFloat} - A matrix that columns are the features and rows are the samples.
    * copydata::Bool = true - If you want to use the same input matrix or a copy.


References
=======

TODO

License
=======

The Perceptrons.jl is free software: you can redistribute it and/or modify it under the terms of the MIT "Expat"
License. A copy of this license is provided in ``LICENSE.md``
