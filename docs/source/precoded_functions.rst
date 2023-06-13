Precoded functions
===================

Listed below are all functions available in PyBEAM's precoded submodule.

.. py:function:: pybeam.precoded.simulate(model, N_sims, phi, dt = 0.0001, seed = False)

   Simulates model N_sims times. Outputs dictionary containing two keys, 'rt_upper' and 'rt_lower', wich contain
   the reaction times for the upper and lower threshold crossing, respectively.
   
   :param model: PyBEAM class object containing model information. See Precoded Tutorial 1 for usage.
   :type model: class

   :param N_sims: Number of accumulators to simulate.
   :type N_sims: int

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter. If keys are unknown for your model, check model class attribute parameters (i.e. run model.parameters()). The output list provides the keys for this dictionary.
   :type phi: dict

   :param dt: Sets the simulation time step. By default, dt = 1.0e-4.
   :type dt: float

   :param seed: Sets the random number seed. Defaults to False. If False, PyBEAM randomly chooses a seed.
   :type seed: int, False

   :return: RT data simulated from your model.
   :rtype: dict (values contain numpy arrays)

.. py:function:: pybeam.precoded.likelihood(model, phi, rt_max, N_tnd = 100, N_mu = 10, x_res = 'default', t_res = 'default', dt_interp_scale = 1.0, dt_interp_overide = 0.0)

   Calculates model likelihood function. Outputs dictionary containing the likelihood function for input models and parameter set.
   Contains three keys: 'time', 'lh_upper', and 'lh_lower'. Value for key 'time'
   corresponds to the time array. Values for keys 'lh_upper' and 'lh_lower' provide the probability
   of crossing the upper and lower thresholds, respectively, at time t provided
   in the 'time' list.

   :param model: PyBEAM class object containing model information. See Precoded Tutorial 1 for usage.
   :type model: class

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter. If keys are unknown for your model, check model class attribute parameters (i.e. run model.parameters()). The output list provides the keys for this dictionary.
   :type phi: dict

   :param rt_max: Sets the time to solve the likelihood function to.
   :type rt_max: float

   :param N_tnd: Sets the number of integration points for the non-decision time distribution. Ignored if model uses constant non-decision time.
   :type N_tnd: int

   :param N_mu: Sets the number of integration points for the drift distribution. Ignored if model uses constant drift rate.
   :type N_mu: int

   :param x_res: Sets the number of spatial mesh points for the PDE solution. Can be set to integer between 101-501, or resolutions 'default' (151), 'fast' (101), 'high' (251), or 'max' (501).
   :type x_res: str, float

   :param t_res: Sets the time resolution for the PDE solution. Can be set to 'default', 'fast', 'high', or 'max'. Should be left at 'default'.
   :type t_res: str

   :param dt_interp_scale: Sets the interpolation resolution. If 1.0, interpolation resolution equals the estimated time step. Otherwise, multiplies estimated time step by this value. Should be left at 1.0.
   :type dt_interp_scale: float

   :param dt_interp_overide: Allows user to automatically set interpolation resolution. If 0.0, interpolation step set by program. Should be left at 0.0.
   :type dt_interp_overide: float

   :return: Model likelihood function.
   :rtype: dict (values contain numpy arrays)

.. py:function:: pybeam.precoded.loglikelihood(model, phi, rt, pointwise = False, N_tnd = 100, N_mu = 10, x_res = 'default', t_res = 'default', dt_interp_scale = 1.0, dt_interp_overide = 0.0)

   Calculates model loglikelihood function. If pointwise = False, outputs sum loglikelihood of all data. If pointwise = True, outputs loglikelihood of each individual data point.

   :param model: PyBEAM class object containing model information. See Precoded Tutorial 1 for usage.
   :type model: class

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter. If keys are unknown for your model, check model class attribute parameters (i.e. run model.parameters()). The output list provides the keys for this dictionary.
   :type phi: dict

   :param rt: Dictionary containing reaction time data.  Must contain two keys, 'rt_upper' and 'rt_lower', with values of numpy arrays/lists containing the upper and lower threshold crossing data.
   :type rt: float

   :param N_tnd: Sets the number of integration points for the non-decision time distribution. Ignored if model uses constant non-decision time.
   :type N_tnd: int

   :param N_mu: Sets the number of integration points for the drift distribution. Ignored if model uses constant drift rate.
   :type N_mu: int

   :param x_res: Sets the number of spatial mesh points for the PDE solution. Can be set to integer between 101-501, or resolutions 'default' (151), 'fast' (101), 'high' (251), or 'max' (501).
   :type x_res: str, float

   :param t_res: Sets the time resolution for the PDE solution. Can be set to 'default', 'fast', 'high', or 'max'. Should be left at 'default'.
   :type t_res: str

   :param dt_interp_scale: Sets the interpolation resolution. If 1.0, interpolation resolution equals the estimated time step. Otherwise, multiplies estimated time step by this value. Should be left at 1.0.
   :type dt_interp_scale: float

   :param dt_interp_overide: Allows user to automatically set interpolation resolution. If 0.0, interpolation step set by program. Should be left at 0.0.
   :type dt_interp_overide: float

   :return: Loglikelihood of RT data.
   :rtype: float (pointwise = False), dict (pointwise = True) with numpy arrays as values

.. py:function:: pybeam.precoded.plot_rt(model, phi, rt_max, rt = False, bins = 25, figsize = (6.4, 4), dpi = 100, N_tnd = 100, N_mu = 10, x_res = 'default', t_res = 'default', dt_interp_scale = 1.0, dt_interp_overide = 0.0)

   Plots the model likelihood function. If input rt is provided a dictionary containing RT data, a histogram of that data is also plotted.

   :param model: PyBEAM class object containing model information. See Precoded Tutorial 1 for usage.
   :type model: class

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter. If keys are unknown for your model, check model class attribute parameters (i.e. run model.parameters()). The output list provides the keys for this dictionary.
   :type phi: dict

   :param rt_max: Sets the time to solve the likelihood function to.
   :type rt_max: float

   :param rt: Dictionary containing reaction time data.  Must contain two keys, 'rt_upper' and 'rt_lower', with values of numpy arrays/lists containing the upper and lower threshold crossing data. If False, will not plot any RT data.
   :type rt: float, False

   :param N_tnd: Sets the number of integration points for the non-decision time distribution. Ignored if model uses constant non-decision time.
   :type N_tnd: int

   :param N_mu: Sets the number of integration points for the drift distribution. Ignored if model uses constant drift rate.
   :type N_mu: int

   :param x_res: Sets the number of spatial mesh points for the PDE solution. Can be set to integer between 101-501, or resolutions 'default' (151), 'fast' (101), 'high' (251), or 'max' (501).
   :type x_res: str, float

   :param t_res: Sets the time resolution for the PDE solution. Can be set to 'default', 'fast', 'high', or 'max'. Should be left at 'default'.
   :type t_res: str

   :param dt_interp_scale: Sets the interpolation resolution. If 1.0, interpolation resolution equals the estimated time step. Otherwise, multiplies estimated time step by this value. Should be left at 1.0.
   :type dt_interp_scale: float

   :param dt_interp_overide: Allows user to automatically set interpolation resolution. If 0.0, interpolation step set by program. Should be left at 0.0.
   :type dt_interp_overide: float

   :return: Figure containing model likelihood and histogram of data (if rt is given a dictionary).
   :rtype: fig

.. py:function:: pybeam.precoded.inference(model, priors, conditions, samples, chains, cores, file_name, dt_interp_scale = 1.0, dt_interp_overide = 0.0, N_tnd = 100, N_mu = 10, sampler = 'DEMetropolisZ', x_res = 'default', t_res = 'default', tune = 0, save_loglikelihood = False)

   Run Bayesian inference on input RT data.

   :param model: PyBEAM class object containing model information. See Precoded Tutorial 1 for usage.
   :type model: class

   :param priors: Dictionary containing parameter priors. Key names are arbitrary. The values for each key are strings written in PyMC's syntax for priors. They can also be constants if you want a parameter to remain fixed at all times.
   :type priors: dict

   :param conditions: Dictionary containing dictionaries for each model condition. See examples for use.
   :type conditions: dict

   :param samples: Sets the number of MCMC samples to run. Recommend at least 25000 samples.
   :type samples: int

   :param chains: Sets the number of MCMC chains to run. Recomend at least 3 chains.
   :type chains: int

   :param cores: Sets the number of cpu cores to run the chains on.
   :type cores: int

   :param file_name: Sets the name of the .nc file output by the solver containing the posteriors. Automatically adds the .nc extension to the string.
   :type file_name: str

   :param dt_interp_scale: Sets the interpolation resolution. If 1.0, interpolation resolution equals the estimated time step. Otherwise, multiplies estimated time step by this value. Should be left at 1.0.
   :type dt_interp_scale: float

   :param dt_interp_overide: Allows user to automatically set interpolation resolution. If 0.0, interpolation step set by program. Should be left at 0.0.
   :type dt_interp_overide: float

   :param N_tnd: Sets the number of integration points for the non-decision time distribution. Ignored if model uses constant non-decision time.
   :type N_tnd: int

   :param N_mu: Sets the number of integration points for the drift distribution. Ignored if model uses constant drift rate.
   :type N_mu: int

   :param sampler: Sets the sampler. Defaults to 'DEMetropolisZ', but can also be set to 'DEMetropolis'.
   :type sampler: str

   :param x_res: Sets the number of spatial mesh points for the PDE solution. Can be set to integer between 101-501, or resolutions 'default' (151), 'fast' (101), 'high' (251), or 'max' (501).
   :type x_res: str, float

   :param t_res: Sets the time resolution for the PDE solution. Can be set to 'default', 'fast', 'high', or 'max'. Should be left at 'default'.
   :type t_res: str

   :param tune: Sets the amount of MCMC tuning steps. Defaults to zero (recommended for DEMetropolisZ and DEMetropolis, but can sometimes be useful. Test on data if need be).
   :type tune: int

   :param save_loglikelihood: If True, saves the loglikelihood of every MCMC sample. Incurs a 2x speed cost.
   :type save_loglikelihood: False, True

   :return: ArViz idata dataframe containing inference information and .nc file which stores it.

.. py:function:: pybeam.precoded.plot_idata(file_name, burnin, combined = False, compact = False)

   Plot Bayesian posteriors output by inference function.

   :param file_name: File name to plot. Input as string omitting .nc extension (automatically added by function).
   :type file_name: str

   :param burnin: Number of samples to throw out from the posterior when plotting.
   :type burnin: int

   :param combined: If False, plots each chain posterior independently. If True, combines the posteriors into one curve.
   :type combined: False, True

   :return: Figure containing Bayesian posteriors.
   :rtype: fig

.. py:function:: pybeam.precoded.summary(file_name, burnin)

   Give summary statistics for Bayesian posteriors given by .nc file.

   :param file_name: File name to plot. Input as string omitting .nc extension (automatically added by function).
   :type file_name: str

   :param burnin: Number of samples to throw out from the posterior when plotting.
   :type burnin: int

   :return: Dataframe containing summary statistics for the input Bayesian posteriors.
