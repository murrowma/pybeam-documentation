Custom functions
================

Listed below are all functions available in PyBEAM's custom submodule.

.. py:function:: pybeam.custom.functions_test(model_dir, phi, x, t)

   Tests user defined model functions to make sure they are operating as expected.

   :param model_dir: String indicating the directory your model files are located in.
   :type model_dir: str

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter.
   :type phi: dict

   :param x: Sets accumulator state to evaluate functions at.
   :type x: float

   :param t: Sets time sot evaluate functions at.
   :type t: float

   :return: Value of each user defined model function at set x and t.
   :rtype: list

.. py:function:: pybeam.custom.simulate(N_sims, model_dir, phi, seed = False, dt = 0.0001)

   Simulates model N_sims times. Outputs dictionary containing two keys, 'rt_upper' and 'rt_lower', wich contain
   the reaction times for the upper and lower threshold crossing, respectively.

   :param N_sims: Number of accumulators to simulate.
   :type N_sims: int

   :param model_dir: String indicating the directory your model files are located in.
   :type model_dir: str

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter.
   :type phi: dict

   :param seed: Sets the random number seed. Defaults to False. If False, PyBEAM randomly chooses a seed.
   :type seed: int, False

   :param dt: Sets the simulation time step. By default, dt = 1.0e-4.
   :type dt: float

   :return: RT data simulated from your model.
   :rtype: dict (values contain numpy arrays)

.. py:function:: pybeam.custom.likelihood(model_dir, phi, rt_max, x_res = 'default', t_res = 'default')

   Calculates model likelihood function. Outputs dictionary containing the likelihood function for input models and parameter set.
   Contains three keys: 'time', 'lh_upper', and 'lh_lower'. Value for key 'time'
   corresponds to the time array. Values for keys 'lh_upper' and 'lh_lower' provide the probability
   of crossing the upper and lower thresholds, respectively, at time t provided
   in the 'time' list.

   :param model_dir: String indicating the directory your model files are located in.
   :type model_dir: str

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter.
   :type phi: dict

   :param rt_max: Sets the time to solve the likelihood function to.
   :type rt_max: float

   :param x_res: Sets the number of spatial mesh points for the PDE solution. Can be set to integer between 101-501, or resolutions 'default' (151), 'fast' (101), 'high' (251), or 'max' (501).
   :type x_res: str, float

   :param t_res: Sets the time resolution for the PDE solution. Can be set to 'default', 'fast', 'high', or 'max'. Should be left at 'default'.
   :type t_res: str

   :return: Model likelihood function.
   :rtype: dict (values contain numpy arrays)

.. py:function:: pybeam.custom.loglikelihood(model_dir, phi, rt, x_res = 'default', t_res = 'default')

   Calculates model loglikelihood.

   :param model_dir: String indicating the directory your model files are located in.
   :type model_dir: str

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter.
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

   :return: Loglikelihood of RT data.
   :rtype: float

.. py:function:: pybeam.custom.plot_rt(model_dir, phi, rt_max, x_res = 'default', t_res = 'default', rt = False, bins = False)

   Plots the model likelihood function. If input rt is provided a dictionary containing RT data, a histogram of that data is also plotted.

   :param model_dir: String indicating the directory your model files are located in.
   :type model_dir: str

   :param phi: Dictionary containing model parameter values. Keys are the model parameters, while values are the value associated with that parameter.
   :type phi: dict

   :param rt_max: Sets the time to solve the likelihood function to.
   :type rt_max: float

   :param rt: Dictionary containing reaction time data.  Must contain two keys, 'rt_upper' and 'rt_lower', with values of numpy arrays/lists containing the upper and lower threshold crossing data. If False, will not plot any RT data.
   :type rt: float, False

   :param x_res: Sets the number of spatial mesh points for the PDE solution. Can be set to integer between 101-501, or resolutions 'default' (151), 'fast' (101), 'high' (251), or 'max' (501).
   :type x_res: str, float

   :param t_res: Sets the time resolution for the PDE solution. Can be set to 'default', 'fast', 'high', or 'max'. Should be left at 'default'.
   :type t_res: str

   :return: Figure containing model likelihood and histogram of data (if rt is given a dictionary).
   :rtype: fig

.. py:function:: pybeam.custom.inference(model_dir, priors, conditions, samples, chains, cores, file_name, solver = 'DEMetropolisZ', x_res = 'default', t_res = 'default', tune = 0, save_loglike = False)

   Run Bayesian inference on input RT data.

   :param model_dir: String indicating the directory your model files are located in.
   :type model_dir: str

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

.. py:function:: pybeam.custom.plot_idata(file_name, burnin, combined = False)

   Plot Bayesian posteriors output by inference function.

   :param file_name: File name to plot. Input as string omitting .nc extension (automatically added by function).
   :type file_name: str

   :param burnin: Number of samples to throw out from the posterior when plotting.
   :type burnin: int

   :param combined: If False, plots each chain posterior independently. If True, combines the posteriors into one curve.
   :type combined: False, True

   :return: Figure containing Bayesian posteriors.
   :rtype: fig

.. py:function:: pybeam.custom.summary(file_name, burnin)

   Give summary statistics for Bayesian posteriors given by .nc file.

   :param file_name: File name to plot. Input as string omitting .nc extension (automatically added by function).
   :type file_name: str

   :param burnin: Number of samples to throw out from the posterior when plotting.
   :type burnin: int

   :return: Dataframe containing summary statistics for the input Bayesian posteriors.
