#include <nucleus/pod.h>

static void xnsched_tt_init(struct xnsched *sched)
{
//	sched_initpq(&sched->rt.runnable, XNSCHED_RT_MIN_PRIO, XNSCHED_RT_MAX_PRIO);
#ifdef CONFIG_XENO_OPT_PRIOCPL
//	sched_initpq(&sched->rt.relaxed, XNSCHED_RT_MIN_PRIO, XNSCHED_RT_MAX_PRIO);
#endif
}

static void xnsched_tt_requeue(struct xnthread *thread)
{
	/*
	 * Put back at same place: i.e. requeue to head of current
	 * priority group (i.e. LIFO, used for preemption handling).
	 */
//	__xnsched_rt_requeue(thread);
}

static void xnsched_tt_enqueue(struct xnthread *thread)
{
	/*
	 * Enqueue for next pick: i.e. move to end of current priority
	 * group (i.e. FIFO).
	 */
//	__xnsched_rt_enqueue(thread);
}

static void xnsched_tt_dequeue(struct xnthread *thread)
{
	/*
	 * Pull from the runnable thread queue.
	 */
//	__xnsched_rt_dequeue(thread);
}

static void xnsched_tt_rotate(struct xnsched *sched,
			      const union xnsched_policy_param *p)
{
/*
 	struct xnthread *thread, *curr;
	struct xnpholder *h;

	if (sched_emptypq_p(&sched->rt.runnable))
		return;	// No runnable thread in this class. 

	curr = sched->curr;

	if (p->rt.prio == XNSCHED_RUNPRIO)
		thread = curr;
	else {
		h = sched_findpqh(&sched->rt.runnable, p->rt.prio);
		if (h == NULL)
			return;
		thread = link2thread(h, rlink);
	}
//*/
	/*
	 * In case we picked the current thread, we have to make sure
	 * not to move it back to the runnable queue if it was blocked
	 * before we were called. The same goes if the current thread
	 * holds the scheduler lock.
	 */
/*	
	if (thread == curr &&
	    xnthread_test_state(curr, XNTHREAD_BLOCK_BITS | XNLOCK))
		return;

	xnsched_putback(thread);

//*/  
}

static struct xnthread *xnsched_tt_pick(struct xnsched *sched)
{
//	return __xnsched_rt_pick(sched);
}

void xnsched_tt_tick(struct xnthread *curr)
{
	/*
	 * The round-robin time credit is only consumed by a running
	 * thread that neither holds the scheduler lock nor was
	 * blocked before entering this callback.
	 */
//	if (likely(curr->rrcredit > 1))
//		--curr->rrcredit;
//	else {
		/*
		 * If the time slice is exhausted for the running
		 * thread, move it back to the runnable queue at the
		 * end of its priority group and reset its credit for
		 * the next run.
		 */
//		curr->rrcredit = curr->rrperiod;
//		xnsched_putback(curr);
	}
}

void xnsched_tt_setparam(struct xnthread *thread,
			 const union xnsched_policy_param *p)
{
//	__xnsched_rt_setparam(thread, p);
}

void xnsched_tt_getparam(struct xnthread *thread,
			 union xnsched_policy_param *p)
{
//	__xnsched_rt_getparam(thread, p);
}

void xnsched_tt_trackprio(struct xnthread *thread,
			  const union xnsched_policy_param *p)
{
//	__xnsched_rt_trackprio(thread, p);
}

#ifdef CONFIG_XENO_OPT_PRIOCPL

static struct xnthread *xnsched_tt_push_rpi(struct xnsched *sched,
					    struct xnthread *thread)
{
//	return __xnsched_rt_push_rpi(sched, thread);
}

static void xnsched_tt_pop_rpi(struct xnthread *thread)
{
//	__xnsched_rt_pop_rpi(thread);
}

static struct xnthread *xnsched_tt_peek_rpi(struct xnsched *sched)
{
//	return __xnsched_rt_peek_rpi(sched);
}

#endif /* CONFIG_XENO_OPT_PRIOCPL */

#ifdef CONFIG_XENO_OPT_VFILE

struct xnvfile_directory sched_tt_vfroot;

struct vfile_sched_tt_priv {
	struct xnholder *curr;
};

struct vfile_sched_tt_data {
	int cpu;
	pid_t pid;
	char name[XNOBJECT_NAME_LEN];
	xnticks_t period;
	int periodic;
	int cprio;
	int dnprio;
};

static struct xnvfile_snapshot_ops vfile_sched_tt_ops;

static struct xnvfile_snapshot vfile_sched_tt = {
	.privsz = sizeof(struct vfile_sched_tt_priv),
	.datasz = sizeof(struct vfile_sched_tt_data),
	.tag = &nkpod_struct.threadlist_tag,
	.ops = &vfile_sched_tt_ops,
};

static int vfile_sched_tt_rewind(struct xnvfile_snapshot_iterator *it)
{
/*
 	struct vfile_sched_rt_priv *priv = xnvfile_iterator_priv(it);
	int nrthreads = xnsched_class_rt.nthreads;

	if (nrthreads == 0)
		return -ESRCH;

	priv->curr = getheadq(&nkpod->threadq);

	return nrthreads;
*/
  
}

static int vfile_sched_tt_next(struct xnvfile_snapshot_iterator *it,
			       void *data)
{
/*
 	struct vfile_sched_rt_priv *priv = xnvfile_iterator_priv(it);
	struct vfile_sched_rt_data *p = data;
	struct xnthread *thread;

	if (priv->curr == NULL)
		return 0;	// All done. 

	thread = link2thread(priv->curr, glink);
	priv->curr = nextq(&nkpod->threadq, priv->curr);

	if (thread->base_class != &xnsched_class_rt)
		return VFILE_SEQ_SKIP;

	p->cpu = xnsched_cpu(thread->sched);
	p->pid = xnthread_user_pid(thread);
	memcpy(p->name, thread->name, sizeof(p->name));
	p->cprio = thread->cprio;
	p->dnprio = xnthread_get_denormalized_prio(thread, thread->cprio);
	p->period = xnthread_get_period(thread);
	p->periodic = xntbase_periodic_p(xnthread_time_base(thread));

	return 1;
//*/
}


static int vfile_sched_tt_show(struct xnvfile_snapshot_iterator *it,
			       void *data)
{
/*
	struct vfile_sched_rt_data *p = data;
	char pribuf[16], ptbuf[16];

	if (p == NULL)
		xnvfile_printf(it, "%-3s  %-6s %-8s %-10s %s\n",
			       "CPU", "PID", "PRI", "PERIOD", "NAME");
	else {
		if (p->cprio != p->dnprio)
			snprintf(pribuf, sizeof(pribuf), "%3d(%d)",
				 p->cprio, p->dnprio);
		else
			snprintf(pribuf, sizeof(pribuf), "%3d", p->cprio);

		xntimer_format_time(p->period, p->periodic, ptbuf, sizeof(ptbuf));

		xnvfile_printf(it, "%3u  %-6d %-8s %-10s %s\n",
			       p->cpu,
			       p->pid,
			       pribuf,
			       ptbuf,
			       p->name);
	}

	return 0;
//*/
  
}

static struct xnvfile_snapshot_ops vfile_sched_tt_ops = {
	.rewind = vfile_sched_tt_rewind,
	.next = vfile_sched_tt_next,
	.show = vfile_sched_tt_show,
};

static int xnsched_tt_init_vfile(struct xnsched_class *schedclass,
				 struct xnvfile_directory *vfroot)
{
/*
	int ret;

	ret = xnvfile_init_dir(schedclass->name, &sched_rt_vfroot, vfroot);
	if (ret)
		return ret;

	return xnvfile_init_snapshot("threads", &vfile_sched_rt,
				     &sched_rt_vfroot);
//*/
  
}

static void xnsched_tt_cleanup_vfile(struct xnsched_class *schedclass)
{
	xnvfile_destroy_snapshot(&vfile_sched_tt);
	xnvfile_destroy_dir(&sched_tt_vfroot);
}

#endif /* CONFIG_XENO_OPT_VFILE */

struct xnsched_class xnsched_class_tt = {
	.sched_init		=	xnsched_tt_init,
	.sched_enqueue		=	xnsched_tt_enqueue,
	.sched_dequeue		=	xnsched_tt_dequeue,
	.sched_requeue		=	xnsched_tt_requeue,
	.sched_pick		=	xnsched_tt_pick,
	.sched_tick		=	xnsched_tt_tick,
	.sched_rotate		=	xnsched_tt_rotate,
	.sched_forget		=	NULL,
	.sched_declare		=	NULL,
	.sched_setparam		=	xnsched_tt_setparam,
	.sched_trackprio	=	xnsched_tt_trackprio,
	.sched_getparam		=	xnsched_tt_getparam,
#ifdef CONFIG_XENO_OPT_PRIOCPL
	.sched_push_rpi 	=	xnsched_tt_push_rpi,
	.sched_pop_rpi		=	xnsched_tt_pop_rpi,
	.sched_peek_rpi 	=	xnsched_tt_peek_rpi,
	.sched_suspend_rpi 	=	NULL,
	.sched_resume_rpi 	=	NULL,
#endif
#ifdef CONFIG_XENO_OPT_VFILE
	.sched_init_vfile	=	xnsched_tt_init_vfile,
	.sched_cleanup_vfile	=	xnsched_tt_cleanup_vfile,
#endif
	.weight			=	XNSCHED_CLASS_WEIGHT(4),
	.name			=	"tt"
};
EXPORT_SYMBOL_GPL(xnsched_class_tt);
