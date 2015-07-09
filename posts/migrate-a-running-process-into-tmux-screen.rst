.. link: http://sayanchowdhury.dgplug.org/migrate-a-running-process-into-tmux.html
.. description: 
.. tags: bookmark, fedora, tmux, planet, screen, reptyr
.. date: 2014/12/27 12:00:00
.. title: Migrate a running process into tmux
.. slug: migrate-a-running-process-into-tmux


Being a regular tmux user. Migrating a running process into tmux using reptyr
comes handy.

`reptyr <https://github.com/nelhage/reptyr>`_ is a utility for taking an existing running program and attaching it to a new terminal. Started a long-running process over ssh, but have to leave and don't want to interrupt it? Just start a screen, use reptyr to grab it, and 
then kill the ssh session and head on home.

The package available in Fedora/Ubuntu repositories.

.. code::

    % sudo yum install -y reptyr        # For Fedora users
    % sudo apt-get install -y reptyr    # For Ubuntu users

The steps to migrate a process is

- Sending the current foreground job to the background using CTRL-Z.
- List all the background jobs using **`jobs -l`**. This will get you the PID 

.. code::

    % jobs -l
    [1]  + 16189 suspended  vim foobar.rst

Here the PID is 16189

- Start a new `tmux` or `screen` session. I will be using `tmux`

.. code::

    % tmux

- Reattach the background process using

.. code::

    % reptyr 16189

If this error appears

.. code::

    Unable to attach to pid 16189: Operation not permitted
    The kernel denied permission while attaching

Then type in the following command as root.

.. code::

    % echo 0 > /proc/sys/kernel/yama/ptrace_scope

These are commands are compatible with screen also
