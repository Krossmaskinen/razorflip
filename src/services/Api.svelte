<script context="module">
    import fetch from 'node-fetch';
    const url = 'https://';

    export const api = {
        saveRazorBladeStatus: (status) => {
            return new Promise((resolve) => {
                const stringifiedStatus = JSON.stringify(status);

                localStorage['razorblade-status'] = stringifiedStatus;

                console.log('status saved');
                resolve();
            });
        },

        getRazorBladeStatus: () => {
            return new Promise((resolve, reject) => {
                const razorbladeStatus = localStorage['razorblade-status'];

                if (razorbladeStatus)
                    resolve(JSON.parse(razorbladeStatus));
                else
                    reject({message: 'No razorblade status found'});
            })
        }
    };
</script>